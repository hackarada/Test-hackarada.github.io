# MASSCAN: Mass IP port scanner

---

[https://github.com/robertdavidgraham/masscan](https://github.com/robertdavidgraham/masscan)

This is an Internet-scale port scanner. It can scan the entire Internet in under 6 minutes, transmitting 10 million packets per second, from a single machine.

It’s input/output is similar to `nmap`, the most famous port scanner. When in doubt, try one of those features.

Internally, it uses asynchronous tranmissions, similar to port scanners like `scanrand`, `unicornscan`, and `ZMap`. It’s more flexible, allowing arbitrary port and address ranges.

NOTE: masscan uses a its own **custom TCP/IP stack**. Anything other than simple port scans may cause conflict with the local TCP/IP stack. This means you need to either the `--src-ip` option to run from a different IP address, or use `--src-port` to configure which source ports masscan uses, then also configure the internal firewall (like `pf` or `iptables`) to firewall those ports from the rest of the operating system.

# Usage

Usage is similar to `nmap`. To scan a network segment for some ports:

    masscan -p80,8000-8100 10.0.0.0/8

This will: * scan the 10.x.x.x subnet, all 16 million addresses * scans port 80 and the range 8000 to 8100, or 102 addresses total * print output to `<stdout>` that can be redirected to a file

To see the complete list of options, use the `--echo` feature. This dumps the current configuration and exits. This output can be used as input back into the program:

    # masscan -p80,8000-8100 10.0.0.0/8 --echo > xxx.conf
    # masscan -c xxx.conf --rate 1000

## Banner checking

Masscan can do more than just detect whether ports are open. It can also complete the TCP connection and interaction with the application at that port in order to grab simple “banner” information.

The problem with this is that masscan contains its own TCP/IP stack separate from the system you run it on. When the local system receives a SYN-ACK from the probed target, it responds with a RST packet that kills the connection before masscan can grab the banner.

The easiest way to prevent this is to assign masscan a separate IP address. This would look like the following:

    # masscan 10.0.0.0/8 -p80 --banners --source-ip 192.168.1.200

The address you choose has to be on the local subnet and not otherwise be used by another system.

In some cases, such as WiFi, this isn’t possible. In those cases, you can firewall the port that masscan uses. This prevents the local TCP/IP stack from seeing the packet, but masscan still sees it since it bypasses the local stack. For Linux, this would look like:

    # iptables -A INPUT -p tcp --dport 61000 -j DROP
    # masscan 10.0.0.0/8 -p80 --banners --source-port 61000

You probably want to pick ports that don’t conflict with ports Linux might otherwise choose for source-ports. You can see the range Linux uses, and reconfigure that range, by looking in the file:

    /proc/sys/net/ipv4/ip_local_port_range

On the latest version of Kali Linux (2018-August), that range is 32768 to 60999, so you should choose ports either below 32768 or 61000 and above.

Setting an `iptables` rule only lasts until the next reboot. You need to lookup how to save the configuration depending upon your distro, such as using `iptables-save` and/or `iptables-persistant`.

On Mac OS X and BSD, there are similar steps. To find out the ranges to avoid, use a command like the following:

    # sysctl net.inet.ip.portrange.first net.inet.ip.portrange.last

On FreeBSD and older MacOS, use an `ipfw` command:

    # sudo ipfw add 1 deny tcp from any to any 40000 in
    # masscan 10.0.0.0/8 -p80 --banners --source-port 40000

On newer MacOS and OpenBSD, use the `pf` packet-filter utility. Edit the file `/etc/pf.conf` to add a line like the following:

    block in proto tcp from any to any port 40000

Then to enable the firewall, run the command:

    # pfctrl -E

If the firewall is already running, then either reboot or reload the rules with the following command:

    # pfctl -f /etc/pf.conf

Windows doesn’t respond with RST packets, so neither of these techniques are necessary. However, masscan is still designed to work best using its own IP address, so you should run that way when possible, even when its not strictly necessary.

The same thing is needed for other checks, such as the `--heartbleed` check, which is just a form of banner checking.

## How to scan the entire Internet

While useful for smaller, internal networks, the program is really designed with the entire Internet in mind. It might look something like this:

    # masscan 0.0.0.0/0 -p0-65535

Scanning the entire Internet is bad. For one thing, parts of the Internet react badly to being scanned. For another thing, some sites track scans and add you to a ban list, which will get you firewalled from useful parts of the Internet. Therefore, you want to exclude a lot of ranges. To blacklist or exclude ranges, you want to use the following syntax:

    # masscan 0.0.0.0/0 -p0-65535 --excludefile exclude.txt

This just prints the results to the command-line. You probably want them saved to a file instead. Therefore, you want something like:

    # masscan 0.0.0.0/0 -p0-65535 -oX scan.xml

This saves the results in an XML file, allowing you to easily dump the results in a database or something.

But, this only goes at the default rate of 100 packets/second, which will take forever to scan the Internet. You need to speed it up as so:

    # masscan 0.0.0.0/0 -p0-65535 --max-rate 100000

This increases the rate to 100,000 packets/second, which will scan the entire Internet (minus excludes) in about 10 hours per port (or 655,360 hours if scanning all ports).

The thing to notice about this command-line is that these are all `nmap` compatible options. In addition, “invisible” options compatible with `nmap` are also set for you: `-sS -Pn -n --randomize-hosts --send-eth`. Likewise, the format of the XML file is inspired by `nmap`. There are, of course, a lot of differences, because the *asynchronous* nature of the program leads to a fundamentally different approach to the problem.

The above command-line is a bit cumbersome. Instead of putting everything on the command-line, it can be stored in a file instead. The above settings would look like this:

    # My Scan
    rate =  100000.00
    output-format = xml
    output-status = all
    output-filename = scan.xml
    ports = 0-65535
    range = 0.0.0.0-255.255.255.255
    excludefile = exclude.txt

To use this configuration file, use the `-c`:

    # masscan -c myscan.conf

This also makes things easier when you repeat a scan.

By default, masscan first loads the configuration file `/etc/masscan/masscan.conf`. Any later configuration parameters override what’s in this default configuration file. That’s where I put my “excludefile” parameter, so that I don’t ever forget it. It just works automatically.

## Getting output

By default, masscan produces fairly large text files, but it’s easy to convert them into any other format. There are five supported output formats:

1. xml: Just use the parameter `-oX <filename>`. Or, use the parameters `--output-format xml` and `--output-filename <filename>`.
2. binary: This is the masscan builtin format. It produces much smaller files, so that when I scan the Internet my disk doesn’t fill up. They need to be parsed, though. The command line option `--readscan` will read binary scan files. Using `--readscan` with the `-oX` option will produce a XML version of the results file.
3. grepable: This is an implementation of the Nmap -oG output that can be easily parsed by command-line tools. Just use the parameter `-oG <filename>`. Or, use the parameters `--output-format grepable` and `--output-filename <filename>`.
4. json: This saves the results in JSON format. Just use the parameter `-oJ <filename>`. Or, use the parameters `--output-format json` and `--output-filename <filename>`.
5. list: This is a simple list with one host and port pair per line. Just use the parameter `-oL <filename>`. Or, use the parameters `--output-format list` and `--output-filename <filename>`. The format is:

        <port state> <protocol> <port number> <IP address> <POSIX timestamp>  
        open tcp 80 XXX.XXX.XXX.XXX 1390380064

## Comparison with Nmap

Where reasonable, every effort has been taken to make the program familiar to `nmap` users, even though it’s fundamentally different. Two important differences are:

- no default ports to scan, you must specify `-p <ports>`
- target hosts are IP addresses or simple ranges, not DNS names, nor the funky subnet ranges `nmap` can use (like `10.0.0-255.0-255`).

You can think of `masscan` as having the following settings permanently enabled: * `-sS`: this does SYN scan only (currently, will change in the future) * `-Pn`: doesn’t ping hosts first, which is fundamental to the async operation * `-n`: no DNS resolution happens * `--randomize-hosts`: scan completely randomized * `--send-eth`: sends using raw `libpcap`

If you want a list of additional `nmap` compatible settings, use the following command:

    # masscan --nmap

## Transmit rate (IMPORTANT!!)

This program spews out packets very fast. On Windows, or from VMs, it can do 300,000 packets/second. On Linux (no virtualization) it’ll do 1.6 million packets-per-second. That’s fast enough to melt most networks.

Note that it’ll only melt your own network. It randomizes the target IP addresses so that it shouldn’t overwhelm any distant network.

By default, the rate is set to 100 packets/second. To increase the rate to a million use something like `--rate 1000000`.
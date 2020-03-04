# Scopping

Resources and tools to help in determining network range and identify machines in the network that we can focus on.

## Tools

- 1. .[Netdiscover](https://github.com/alexxy/netdiscover)

    Netdiscover is a network address discovering tool, developed mainly for those wireless networks without dhcp server, it also works on hub/switched networks. Its based on arp packets, it will send arp requests and sniff for replies.

    ### Examples

    scan common lan addresses on eth0

        netdiscover -i eth0

    Fast scan common lan addresses on eth0 (search only for gateways)

        netdiscover -i eth0 -f

    Scan some fixed ranges

        netdiscover -i eth0 172.26.0.0/24
        netdiscover -i eth0 192.168.0.0/16
        netdiscover -i eth0 10.0.0.0/8

    Scan common lan addresses with sleep time 0.5 instead of default 1

        netdiscover -i eth0 -s 0.5

    Scan fixed range on fast mode with sleep time 0.5 instead of default 1

        netdiscover -i eth0 192.168.0.0/16 -f -s 0.5

    Only sniff for arp traffic, dont send nothing

        netdiscover -i eth0 -p

    Scan for common lan addresses using old hardcore mode (much more faster, but avoid it on networks with bad link).

        netdiscover -i eth0 -S

- 2 , [MASS](https://github.com/robertdavidgraham/masscan](https://github.com/robertdavidgraham/masscan))[CAN](https://github.com/robertdavidgraham/masscan)

    MASSCAN is an Internet-scale port scanner. It can scan the entire Internet in under 6 minutes, transmitting 10 million packets per second, from a single machine.

    ### Usage

    Usage is similar to `nmap`. To scan a network segment for some ports:

        masscan -p80,8000-8100 10.0.0.0/8

    This will: * scan the 10.x.x.x subnet, all 16 million addresses * scans port 80 and the range 8000 to 8100, or 102 addresses total * print output to `<stdout>` that can be redirected to a file

    To see the complete list of options, use the `--echo` feature. This dumps the current configuration and exits. This output can be used as input back into the program:

        # masscan -p80,8000-8100 10.0.0.0/8 --echo > xxx.conf
        # masscan -c xxx.conf --rate 1000

## Notes

Resolve to a local server name : -Update host

    vim /etc/hosts
    
    ipaddress name

[MASSCAN: Mass IP port scanner](Scopping/MASSCAN%20Mass%20IP%20port%20scanner.md)

[Netdiscover](Scopping/Netdiscover.md)
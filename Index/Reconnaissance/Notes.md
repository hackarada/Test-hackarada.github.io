# Notes

---

- Idnetify

        Initial perimeter scan
        
        Fast scan common lan
        netdiscover -i eth0 -f
        scan range
        netdiscover -i eth0 -r 192.168.61.0/24
        
        
        docker run -it --privileged --net=host bettercap/bettercap -h
        

- Recon target

        nmap -sV -p- [target]
        
        FullScan
        sudo nmap -sS -sU -T4 -A -v -PE -PP -PS21,22,23,25,80,113,31339 -PA80,113,443,10042 -PO --script all

    Basic Nmap recon

        nmap -sV -sC -oA ~/nmap-1[ip]
        
        -sV : Probe open ports to determine service/version info
        -sC : to enable the script
        -oA : to save the results
        
        After this quick command you can add "-p-" to run a full scan while you work with the previous result

- recon-ng

        test@ubuntu:~/$ git clone https://github.com/lanmaster53/recon-ng.git
        test@ubuntu:~/$ cd recon-ng
        	test@ubuntu:~/recon-ng/$ pip install -r REQUIREMENTS

    apt-get update && apt-get install recon-ng
# Passive Information Gathering

information gathering to discover preliminary information about the systems, their software and the people involved with the target.

Website Recon
Whois Enumeration
Google Hacking
Netcraft
Recon-ng
Open-Source Code
Shodan
Security Headers Scanner
SSL Server Test
Pastebin
User Information Gathering
Email Harvesting
Password Dumps
Social Media Tools
Site-Specific Tools
Stack Overflow
Information Gathering Frameworks
OSINT Framework
Maltego

## Passive recon

- Using Shodan (https://www.shodan.io/) to detect similar app

        can be integrated with nmap (https://github.com/glennzw/shodan-hq-nse)nmap --script shodan-hq.nse --script-args 'apikey=<yourShodanAPIKey>,target=<hackme>'

- Using The Wayback Machine (https://archive.org/web/) to detect forgotten endpoints

        look for JS files, old links

- Using The Harvester (https://github.com/laramies/theHarvester)

        python theHarvester.py -b all -d domain.com

## Ref

1. [https://resources.infosecinstitute.com/information-gathering](https://resources.infosecinstitute.com/information-gathering)

[OSINT](Passive%20Information%20Gathering/OSINT.md)
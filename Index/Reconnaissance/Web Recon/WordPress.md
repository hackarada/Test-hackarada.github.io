# WordPress

---

    
    #Scan installed plugins
    wpscan --url http(s)://your-domain.com --enumerate p
    
    #Scan vulnerable plugins
    wpscan --url http(s)://your-domain.com --enumerate vp
    
    #Scan installed themes
    wpscan --url http(s)://your-domain.com --enumerate t
    
    #Scan vulnerable themes
    wpscan --url http(s)://your-domain.com --enumerate vt
    
    #Scan user accounts:
    wpscan --url http(s)://your-domain.com --enumerate u
    
    #Scan vulnerable timthumb files:
    wpscan --url http(s)://your-domain.com --enumerate tt

Using WPVulnDB API

    nano ~/.wpscan/scan.yml

Put the following lines in the file.

[https://wpvulndb.com/users/edit](https://wpvulndb.com/users/edit)

    cli_options:
        api_token: YOUR_API_TOKEN

Add this to update database and wpscan daily

    @daily /usr/local/bin/wpscan --update && gem update wpscan

Issues

    # Issue when using config files
    Scan Aborted: undefined method `deep_symbolize_keys'
    #solution
    

my

    wpscan --url [http://192.168.61.222](http://192.168.61.222/) --api-token --enumerate u p

## References

1. [https://www.linuxbabe.com/security/install-wpscan-wp-vulnerability-scanner](https://www.linuxbabe.com/security/install-wpscan-wp-vulnerability-scanner)
# Web Recon

---

 WordPress sites

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

## References

1. [https://www.linuxbabe.com/security/install-wpscan-wp-vulnerability-scanner](https://www.linuxbabe.com/security/install-wpscan-wp-vulnerability-scanner)

[WordPress ](Web%20Recon/WordPress.md)
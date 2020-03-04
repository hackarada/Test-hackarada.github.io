# Archives

---

**Compressing archives**

    tar -zcvf test.tar test
    
    gzip test
    
    zip -9 test.zip test
    
    zip -r test.zip test/

# Extracting archives

    tar xvfj test.tar.bz2
    tar zxvf test.tar.gz
    tar zxvf test.tar
    gzip -d test.gz
    unzip test.zip
    zcat rockyou.txt.gz > rockyou.txt
    

# Compressing archives

    tar -zcvf test.tar test
    gzip test
    zip -9 test.zip test
    zip -r test.zip test/
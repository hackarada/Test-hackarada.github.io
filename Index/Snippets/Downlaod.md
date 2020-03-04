# Downlaod

---

### Copy remote file to local

    scp /path/to/local/file.txt user@targetIP:/path/to/share # local to remote

    scp -r user@targetIP:/path/to/share /local/share # remote to local

    cat ~/.ssh/id_rsa.pub | ssh user@targetIP 'cat >> .ssh/authorized

# Copy files remotely

    scp /path/to/local/file.txt user@targetIP:/path/to/share # local to remote
    scp -r user@targetIP:/path/to/share /local/share # remote to local
    cat ~/.ssh/id_rsa.pub | ssh user@targetIP 'cat >> .ssh/authorized_keys'
    

# File Permissions
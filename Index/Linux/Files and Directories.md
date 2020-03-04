# Files and Directories

---

Current Working Directory

    pwd

change directory

    cd ~
    * ~ is for home directory
    * / is for root directory

### Viewing File Permissions

 view the permissions on a file or director

    ls -l <directory/file>

    -rw-r--r-- 1 root root 1031 Nov 18 09:22 /etc/passwd

The first ten characters show the access permissions. 

The first dash (-) indicates the type of file (d for directory, s for special file, and - for a regular file). 

The next three characters (rw-) define the owner’s permission to the file. In this example, the file owner has read and write permissions only. 

The next three characters (r–) are the permissions for the members of the same group as the file owner (which in this example is read only). 

The last three characters (r–) show the permissions for all other users and in this example it is read only.

    drwxr-xr-x 2 user user 4096 Jan 9 10:11 documents

`drwxr-xr-x` are the permissions

`2` is the number of files or directories

`user` is the owner

`user` is the group

`4096` is the size`   -- **Since a directory itself is a file, any directory will always show 4096 as it’s size. This does not reflect the size of the contents of the directory.**

Jan 9 10:11`  is the date/time of last access

`documents` is the directory

## Changing Directory and File Permissions

- chmod – change permissions

    Read - 4

    write - 2 

    execute -1 

        chmod 777 
        # Everybody can do everything to this file.
        #{7 -current user }
        #{7 -current group }
        #{7 -current others}

        chmod 700 file
        #Protects a file against any access from other users, while the issuing user still has full access.

    The format of a symbolic mode is [ugoa...][[+-=][perms...]...], where perms is either zero or more letters from the set rwxXst, or a single letter from the set ugo. Multiple symbolic modes can be given, separated by commas.

    To allow yourself to execute a file that you own named `myfile`, enter:

        chmod u+x myfile
        

    To allow anyone who has access to the directory in which `myfile` is stored to read or execute `myfile`, enter:

        chmod o+rx myfile

        sudo chmod -R ugo+rw /DATA/SHARE
        * R – this modifies the permission of the parent folder and the child objects within (Recursive)
        
        * ugo+rw – this gives User, Group, and Other read and write access.

    - For file `myfile`, to grant read, write, and execute permissions to yourself (4+2+1=7), read and execute permissions to users in your group (4+0+1=5), and only execute permission to others (0+0+1=1), you would use:

            chmod 751 myfile

- chown – change ownership.

        sudo chown -R bethany /DATA/SHARE

## Reference

[https://linux.die.net/man/1/chmod](https://linux.die.net/man/1/chmod)

[https://kb.iu.edu/d/abdb](https://kb.iu.edu/d/abdb)

[https://www.linuxtopia.org/online_books/introduction_to_linux/linux_The_chmod_command.html](https://www.linuxtopia.org/online_books/introduction_to_linux/linux_The_chmod_command.html)
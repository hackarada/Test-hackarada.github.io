# Storage

---

### Expand Hard Hardisk on virtualBox

Ref

1. [https://askubuntu.com/questions/101715/resizing-virtual-drive/558215#558215](https://askubuntu.com/questions/101715/resizing-virtual-drive/558215#558215)
2. 2. [https://askubuntu.com/questions/88647/how-do-i-increase-the-hard-disk-size-of-the-virtual-machine](https://askubuntu.com/questions/88647/how-do-i-increase-the-hard-disk-size-of-the-virtual-machine)

    
    VBoxManage modifyhd YOUR_HARD_DISK.vdi --resize SIZE_IN_MB
    open Gparted and expand hard disk
    

- Detail

    This answer is directed at a Windows host, but if you use bash in place of the PowerShell and replace '\' with '/' it should work just fine.

    Enlarge virtual drive

    1. **From VirtualBox**
        1. Release the VDI file: File -> Virtual Media Manager -> Select VDI -> Release
        2. Copy the location of the VDI inside the properties box 'C:\Users\campbell\VirtualBox VMs\Ubuntu14\Ubuntu14.vdi'
        3. Backup the VDI file
            1. Copy the VDI file to a new location.
            2. Assign a new UUID to the original VDI file:
                1. Start `Powershell` (not as an administrator):
                2. Change to your Oracle VirtualBox directory `cd C:\Program Files\Oracle\VirtualBox`
                3. `.\VBoxManage.exe internalcommands sethduuid "C:\Users\campbell\VirtualBox VMs\Ubuntu14\Ubuntu14.vdi"`
        4. Remove and re-add your machine's .vdi file to update its UUID.
            1. File -> Virtual Media Manager -> Select VDI -> Remove
            2. Apply.
            3. Right click your VM -> Configuration -> Storage -> Controller: SATA -> Add new hard drive. Select your .vdi file.
    2. **From host**
        1. Work out desired size: you can google it, eg. '40 Gb=MB' returns 40000 MB
        2. Start `PowerShell` (not as administrator)
        3. Change to your Oracle VirtualBox directory `cd C:\Program Files\Oracle\VirtualBox`
        4. Resize your .vdi file `.\VBoxManage.exe modifyhd "C:\Users\campbell\VirtualBox VMs\Ubuntu14\Ubuntu14.vdi" --resize 40000`
        5. Now start your virtual machine. You will receive the same warning about space that prompted you to engage in this procedure. Not to worry, we are near the end.
    3. **On your virtual machine**
        1. Start the partition manager `gparted` (install it if is is missing `sudo apt-get install gparted`)
        2. Get rid of the swap partition, which prevents you from expanding the root partition. Note that you cannot harm the rest of your machine - this is all happening inside a single file. Worst case scenario you trash this file and you have to use your backup instead.
            1. Make a note of the size of the linux-swap partition 4 GiB in my case
            2. Right click on it and `Swapoff`
            3. Right click on it and `Delete`
            4. Apply by clicking on the checkmark (Apply all operations). Ignore the dire warning - life is too short to indulge Cassandras
            5. right click on the extended file system that once housed the swap partition (/dev/sda2 in all likelihood) and delete it
            6. right click on the root partition (/dev/sda1) and resize it. Tab to the 'Free space following' field and enter the size of the swap partition. Shift-Tab and the machine will work out the new size for you automatically.
            7. Right click in the unallocated space at the end and make it an extended partition
            8. Right click in the new partition and select `linux-swap` in the File system field.
            9. Commit your changes as before
            10. Right click on your swap partition and select `swapon`
            11. Tell the Fat Lady to commence singing.

### References:

1. [https://tinyapps.org/blog/misc/201204120700_virtualbox_increase_disk_space.html](https://tinyapps.org/blog/misc/201204120700_virtualbox_increase_disk_space.html)
2. [Resize Ubuntu 10.04 VirtualBox VM virtual disk](https://askubuntu.com/questions/219880/resize-ubuntu-10-04-virtualbox-vm-virtual-disk)
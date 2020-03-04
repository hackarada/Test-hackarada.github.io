# Networking

IP address

    ifconfig [interface]
    
    ip a s dev [interface]

Turn interface down

    ifdown [interface]

turn interface up

    ifup [interface]

change IP

    ifconfig eth0:0 10.104.33.39 
     * this will be reset back after ifdown /reboot
    to have a presistante IP
    
    add it to  /etc/network/interfaces file
    
    root@server42:~# tail -4 /etc/network/interfaces
    auto eth0:0
    iface eth0:0 inet static
    **address 10.104.33.39
    netmask 255.255.0.0
    
    
    Note:  use
    nmtui 
    to mange networking with GUI**

restart network

    systemctl restart network
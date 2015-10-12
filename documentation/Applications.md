Applications
==

    root@edison:~# journalctl
    root@edison:~# cat /etc/modprobe.d/bcm4334x.conf 
    options bcm4334x firmware_path=/etc/firmware/fw_bcmdhd.bin nvram_path=/etc/firmware/bcmdhd.cal op_mode=4
    root@edison:~# cat /etc/modprobe.d/g_multi.conf  
    options g_multi file=/dev/mmcblk0p9 stall=0 idVendor=0x8087 idProduct=0x0A9E iProduct=Edison iManufacturer=Intel
    
## Links

- http://dev.ardupilot.com/wiki/edison-for-drones/
- https://github.com/catmaker/chippy



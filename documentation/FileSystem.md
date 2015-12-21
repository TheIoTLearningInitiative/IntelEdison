File System
==

    user@host:~$ nano edison-src/device-software/meta-edison-distro/recipes-bsp/u-boot/files/edison.env
    user@host:~$ nano edison-src/device-software/meta-edison/recipes-bsp/u-boot/files/edison.env
    user@host:~$ nano edison-src/meta-intel-edison/meta-intel-edison-bsp/recipes-bsp/u-boot/files/edison.env
    Rootfs’ size from 512MB to 1312MB
    user@host:~$ nano edison-src/meta-intel-edison/meta-intel-edison-distro/recipes-core/images/edison-image.bb
    rootfs 1312MB
    user@host:~$ /device-software/utils/flash/postBuild.sh
    user@host:~# apt-get install dfu-util
    user@host:~$ /build/toFlash/flashall.sh --recovery
    user@host:~$ /build/toFlash/flashall.sh
    user@host:~# screen /dev/ttyUSBX 115200
    root@edison:~# df -h
    
## Free Space

### Yocto, Fresh Installation



### Ubilinux, Fresh Installation

    edison@ubilinux:~$ df -h
    Filesystem       Size  Used Avail Use% Mounted on
    rootfs           1.4G  812M  504M  62% /
    /dev/root        1.4G  812M  504M  62% /
    devtmpfs         480M     0  480M   0% /dev
    tmpfs             97M  292K   96M   1% /run
    tmpfs            5.0M     0  5.0M   0% /run/lock
    tmpfs            193M     0  193M   0% /run/shm
    tmpfs            481M     0  481M   0% /tmp
    /dev/mmcblk0p7    32M  5.3M   27M  17% /boot
    /dev/mmcblk0p10  1.3G  2.0M  1.3G   1% /home

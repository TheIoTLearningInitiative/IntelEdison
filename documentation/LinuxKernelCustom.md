Linux Kernel
==

## Building via Make

    user@host:~$ pwd
    /home/xe1gyq/Projects/edison-src
    user@host:~$ cd out/current
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake virtual/kernel -c menuconfig
    ...
    edison-src/out/linux64/build/tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/Makefile
    user@host:~$ bitbake virtual/kernel -c configure -f -v
    user@host:~$ cd ../../..
    user@host:~$ make image
    user@host:~$ make flash
    
## Building via BitBake (Unchecked)

    user@host:~$ pwd
    /home/xe1gyq/Projects/edison-src
    user@host:~$ cd out/current
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake virtual/kernel -c menuconfig
    ...
    edison-src/out/linux64/build/tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/Makefile
    user@host:~$ bitbake virtual/kernel -c configure -f -v
    user@host:~$ bitbake edison-image
    
    

## Others

    user@host:~$ nano edison-src/meta-intel-edison/meta-intel-edison-bsp/recipes-kernel/linux/files/defconfig
    user@host:~$ nano edison-src/meta-intel-edison/meta-intel-edison-bsp/recipes-kernel/linux/files/upstream_to_edison.patch
    user@host:~$ find -name 
    user@host:~$ cp /build/tmp/work/edison-poky-linux/linuxyocto/3.10.17+gitAUTOINC+6ad20f049a_c03195ed6e-r0/linux-edison-standardbuild/.config build/tmp/work/edison-poky-linux/linuxyocto/3.10.17+gitAUTOINC+6ad20f049a_c03195ed6er0/defconfig

## Links

- [Yocto Project Linux Kernel Development Manual](http://www.yoctoproject.org/docs/latest/kernel-dev/kernel-dev.html)

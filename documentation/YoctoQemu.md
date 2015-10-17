# Yocto Qemu

    user@host:~# apt-get install gawk wget git-core diffstat unzip texinfo build-essential
    user@host:~# apt-get install qemu
    user@host:~$ git clone git://git.yoctoproject.org/poky --branch daisy
    user@host:~$ source poky/oe-init-build-env yocto-x86-minimal
    user@host:~$ bitbake core-image-minimal
    user@host:~$ bitbake core-image-full-cmdline-x86
    user@host:~$ runqemu qemux86
    
    user@host:~$ mkdir source
    user@host:~$ cd source
    user@host:~$ git clone -b daisy git://git.yoctoproject.org/poky
    user@host:~$ git clone -b daisy git://git.yoctoproject.org/meta-intel
    user@host:~$ source poky/oe-init-build-env yocto-x86-minnowmax
    user@host:~$ bitbake core-image-sato-sdk
    $ sudo apt-get install gawk wget git-core diffstat unzip texinfo build-essential chrpath
    Reading package lists... Done
    Building dependency tree     
    Reading state information... Done
    ... ...
    0 upgraded, 0 newly installed, 0 to remove and 535 not upgraded.
    xe1gyq@sayulita:~$ git clone git://git.yoctoproject.org/poky --branch daisy
    user@host:~$ sudo apt-get install qemu
    git clone git://git.yoctoproject.org/poky --branch daisy
    Cloning into 'poky'...
    remote: Counting objects: 240747, done.
    remote: Compressing objects: 100% (59908/59908), done.
    Receiving objects:  20% (48390/240747), 25.06 MiB | 604 KiB/s
    ... ...
    user@host:~$ source poky/oe-init-build-env yocto-x86
    user@host:~$ bitbake core-image-minimal
    user@host:~$ bitbake core-image-full-cmdline-x86
    user@host:~$ runqemu qemux86
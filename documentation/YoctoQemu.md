# Yocto Qemu

    user@host:~# apt-get install gawk wget git-core diffstat unzip texinfo build-essential chrpath
    user@host:~# apt-get install qemu
    user@host:~$ git clone git://git.yoctoproject.org/poky --branch fido
    user@host:~$ source poky/oe-init-build-env yocto-x86-minimal
    user@host:~$ bitbake core-image-minimal
    user@host:~$ bitbake core-image-full-cmdline-x86
    user@host:~$ runqemu qemux86
    
    user@host:~$ mkdir source
    user@host:~$ cd source
    user@host:~$ git clone -b fido git://git.yoctoproject.org/poky
    user@host:~$ git clone -b fido git://git.yoctoproject.org/meta-intel
    user@host:~$ source poky/oe-init-build-env yocto-x86-minnowmax
    user@host:~$ bitbake core-image-sato-sdk

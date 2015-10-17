## Yocto Qemu

    user@host:~# apt-get install gawk wget git-core diffstat unzip texinfo build-essential chrpath
    user@host:~# apt-get install qemu
    user@host:~$ git clone git://git.yoctoproject.org/poky --branch fido
    user@host:~$ source poky/oe-init-build-env yocto-x86-minimal
    user@host:~$ bitbake core-image-minimal
    user@host:~$ bitbake core-image-full-cmdline-x86
    user@host:~$ bitbake core-image-sato-sdk
    user@host:~$ runqemu qemux86

## Yocto Minnowboard MAX

    user@host:~$ mkdir source
    user@host:~$ cd source
    user@host:~$ git clone -b fido git://git.yoctoproject.org/poky
    user@host:~$ cd poky
    user@host:~$ git clone -b fido git://git.yoctoproject.org/meta-intel
    user@host:~$ source oe-init-build-env yocto-x86-minnowmax
    user@host:~$ bitbake-layers add-layer "$HOME/source/poky/meta-intel"
    user@host:~$ echo 'MACHINE = "intel-corei7-64"' >> conf/local.conf
    user@host:~$ bitbake core-image-minimal
    user@host:~$ ls tmp/deploy/images/intel-corei7-64/
    ...
    core-image-minimal-intel-corei7-64.hddimg
    $ sudo $HOME/source/poky/scripts/contrib/mkefidisk.sh HOST_DEVICE \
    tmp/deploy/images/intel-corei7-64/core-image-minimal-intel-corei7-64.hddimg \
    TARGET_DEVICE

## Links

- [Yocto Project @ Minnowboard MAX](http://wiki.minnowboard.org/Yocto_Project)
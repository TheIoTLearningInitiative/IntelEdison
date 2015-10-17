# Yocto Qemu

    $ sudo apt-get install gawk wget git-core diffstat unzip texinfo build-essential
    $ sudo apt-get install qemu
    $ git clone git://git.yoctoproject.org/poky --branch daisy
    $ source poky/oe-init-build-env yocto-x86-minimal
    $ bitbake core-image-minimal
    $ bitbake core-image-full-cmdline-x86
    $ runqemu qemux86
    $ mkdir source
    $ cd source
    $ git clone -b daisy git://git.yoctoproject.org/poky
    $ git clone -b daisy git://git.yoctoproject.org/meta-intel
    $ source poky/oe-init-build-env yocto-x86-minnowmax
    $ bitbake core-image-sato-sdk
    $ sudo apt-get install gawk wget git-core diffstat unzip texinfo build-essential chrpath
    Reading package lists... Done
    Building dependency tree     
    Reading state information... Done
    ... ...
    0 upgraded, 0 newly installed, 0 to remove and 535 not upgraded.
    xe1gyq@sayulita:~$ git clone git://git.yoctoproject.org/poky --branch daisy
    $sudo apt-get install qemu
    git clone git://git.yoctoproject.org/poky --branch daisy
    Cloning into 'poky'...
    remote: Counting objects: 240747, done.
    remote: Compressing objects: 100% (59908/59908), done.
    Receiving objects:  20% (48390/240747), 25.06 MiB | 604 KiB/s
    ... ...
    $ source poky/oe-init-build-env yocto-x86
    $ bitbake core-image-minimal
    $ bitbake core-image-full-cmdline-x86
    $ runqemu qemux86
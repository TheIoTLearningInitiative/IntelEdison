Yocto Edison
==

The Intel® Edison Board Support Package offers these features:

- Kernel image based on Linux kernel 3.10.17
- U-boot second stage bootloader
- Bluetooth and Wi-Fi connectivity
- Intel cloud connectivity middleware
- Many base Linux packages provided by the Yocto project

[Board Support Package (BSP) User Guide for Boards and Kits](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005616.html)

## Dependencies

    user@host:~# apt-get install build-essential git diffstat gawk chrpath texinfo libtool gcc-multilib dfu-util screen u-boot-tools

## Board Support Package

### Download

Go to [Intel® Edison Board Software Downloads](https://software.intel.com/en-us/iot/hardware/edison/downloads)
and copy the link location for "Sources - Linux Sources Files" then download them

    user@host:~$ wget http://downloadmirror.intel.com/25028/eng/edison-src-ww25.5-15.tgz

### Building via Make

    user@host:~$ tar xvf edison-src-ww25.5-15.tgz
    user@host:~$ cd edison-src
    user@host:~$ pwd
    /home/xe1gyq/Projects/edison-src
    user@host:~$ ls
    Makefile  meta-intel-edison
    user@host:~$ make setup
    abraham@aarcemor-desk:~/edison-src$ make setup
    Setup buildenv for SDK host linux64
    ./meta-intel-edison/setup.sh  --dl_dir=/home/abraham/edison-src/bbcache/downloads --sstate_dir=/home/abraham/edison-src/bbcache/sstate-cache --build_dir=/home/abraham/edison-src/out/linux64 --build_name=custom_build_aarcemor@20151220153244 --sdk_host=linux64
    We are building in external mode
    Fetching origin
    Fetching origin
    Fetching origin
    Fetching origin
    Cloning Poky in the /home/abraham/edison-src/out/linux64/poky directory
    Cloning into 'poky'...
    done.
    Note: checking out 'yocto-1.7.2'.
    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.
    
    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:

      git checkout -b new_branch_name

    HEAD is now at 29812e6... busybox: unbreak tar of uncompressed files
    Cloning Mingw layer to /home/abraham/edison-src/out/linux64/poky/meta-mingw directory from local cache
    Cloning into 'meta-mingw'...
    done.
    Cloning Darwin layer to /home/abraham/edison-src/out/linux64/poky/meta-darwin directory from local cache
    Cloning into 'meta-darwin'...
    done.
    Note: checking out '29b5ff31cee24e796f2eb2d2fd1269e3e92c831c'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.
    
    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:

      git checkout -b new_branch_name

    HEAD is now at 29b5ff3... gcc-runtime: Don't pollute global export namespace
    Cloning meta-intel-iot-middleware layer to /home/abraham/edison-src/out/linux64/poky/meta-intel-iot-middleware directory from local cache
    Cloning into 'meta-intel-iot-middleware'...
    done.
    Note: checking out 'c6d681475e76107e6c04c5f7a06034dc9e772d1e'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.

    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:

      git checkout -b new_branch_name

    HEAD is now at c6d6814... upm: Update to 0.3.1
    Cloning meta-arduino layer to /home/abraham/edison-src directory from GitHub.com/01org/meta-arduino
    Cloning into 'meta-arduino'...
    remote: Counting objects: 72, done.
    remote: Total 72 (delta 0), reused 0 (delta 0), pack-reused 72
    Unpacking objects: 100% (72/72), done.
    Checking connectivity... done.
    Already on '1.6.x'
    Your branch is up-to-date with 'origin/1.6.x'.
    Applying patch on poky
    Initializing yocto build environment
    Setting up yocto configuration file (in build/conf/local.conf)
    ** Success **
    SDK will be generated for linux64 host
    Now run these two commands to setup and build the flashable image:
    cd /home/abraham/edison-src/out/linux64
    source poky/oe-init-build-env
    bitbake edison-image
    *************


    user@host:~$ ls
    bbcache  Makefile  meta-arduino  meta-intel-edison  out  pub
    user@host:~$ make image
    user@host:~$ ls
    bbcache  Makefile  meta-arduino  meta-intel-edison  out  pub
    user@host:~$ make flash
    ...
    U-boot & Kernel System Flash Success...
    Your board needs to reboot to complete the flashing procedure, please do not unplug it for 2 minutes.
    ...
    user@host:~$ ls
    bbcache  flash.log  Makefile  meta-arduino  meta-intel-edison  out  pub
    user@host:~$ cd out/current
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake virtual/kernel -c menuconfig
    user@host:~$ bitbake virtual/kernel -c configure -f -v
    user@host:~$ bitbake edison-image

### Building via Make + Bitbake

    user@host:~$ tar xvf edison-src-ww25.5-15.tgz
    user@host:~$ cd edison-src
    user@host:~$ ls
    Makefile  meta-intel-edison
    user@host:~$ make setup
    user@host:~$ ls
    bbcache  Makefile  meta-arduino  meta-intel-edison  out  pub
    user@host:~$ cd out/linux64 || cd out/current
    user@host:~$ ls
    build  poky
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake edison-image
    user@host:~$ ls
    arduino  bbcache  broadcom_cws  device-software  Makefile  meta-arduino meta-intel-edison  mw  out  pub
    user@host:~$ cd out/linux64/build/tmp/deploy/images/edison
    user@host:~$ cd meta-intel-edison/utils/flash
    user@host:~$ ls edison-src/build/tmp/deploy/images/edison/edison-image-edison.hddimg

### Building via Script

    user@host:~$ tar xvf edison-src-ww25.5-15.tgz
    user@host:~$ cd edison-src
    user@host:~$ pwd
    /home/xe1gyq/Projects/edison-src
    user@host:~$ ls
    Makefile  meta-intel-edison
    user@host:~$ mkdir bitbake_download_dir
    user@host:~$ mkdir bitbake_sstate_dir
    user@host:~$ ./meta-intel-edison/setup.sh --dl_dir=bitbake_download_dir --sstate_dir=bitbake_sstate_dir
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake edison-image
    user@host:~$ ../meta-intel-edison/utils/flash/postBuild.sh .
    user@host:~# apt-get install dfu-util
    user@host:~$ build/toFlash/flashall.sh --recovery
    user@host:~$ build/toFlash/flashall.sh

- user@host:~$ ./device-software/setup.sh
- File name: edison-src-weekly-68.tgz @ https://downloadcenter.intel.com/download/24357
- https://scratchbuffer.wordpress.com/2015/09/01/yocto-linux-image-build-for-intel-edison-simple-and-easy/
- https://wiki.lsr.ei.tum.de/nst/documentation/inteledison
- https://hayestech.wordpress.com/2015/01/26/building-custom-intel-edison-images/

## Native SDK

### Building via Make

    user@host:~$ make sdk
    user@host:~$ ls out/current/build/tmp/deploy/sdk/
    poky-edison-glibc-x86_64-edison-image-core2-32-toolchain-1.7.2.manifest
    poky-edison-glibc-x86_64-edison-image-core2-32-toolchain-1.7.2.sh
    user@host:~$ out/current/build/tmp/deploy/sdk/poky-edison-glibc-x86_64-edison-image-core2-32-toolchain-1.7.2.sh

### Building via BitBake

    user@host:~$ bitbake edison-image-c populate_sdk
    user@host:~$ ls tmp/deploy/sdk
    user@host:~$ poky-edison-eglibc-x86_64-edison-image-core2-32-toolchain-1.6.1.sh

## Packages Standard

    user@host:~$ nano edison-src/meta-intel-edison/meta-intel-edison-distro/recipes-core/images/edison-image.bb
    IMAGE_INSTALL += “libpng”
    IMAGE_INSTALL += "opencv"
    PACKAGE_EXCLUDE = "libpng"

## Packages Third Party, AX25

    user@host:~$ pwd
    edison-src/out/linux64/build
    user@host:~$ cd edison-src/out/current/poky
    user@host:~$ git clone https://github.com/hambedded-linux/meta-hamradio.git
    user@host:~$ nano edison-src/out/current/build/conf/bblayers.conf
    /home/xe1gyq/Projects/edison-src/out/linux64/poky/meta-hamradio
    user@host:~$ rm -rf /home/xe1gyq/Projects/edison-src/out/linux64/poky/meta-hamradio/recipes-kernel
    user@host:~$ nano meta-intel-edison/meta-intel-edison-distro/recipes-core/images/edison-image.bb
    IMAGE_INSTALL += “ax25-apps”
    IMAGE_INSTALL += “ax25-tools”
    IMAGE_INSTALL += “libax25”
    user@host:~$ make image
    user@host:~$ make flash

### Tbd

    user@host:~$ cd edison-src/meta-intel-edison/
    user@host:~$ git clone https://github.com/openembedded/meta-openembedded.git
    user@host:~$ cd meta-openembedded/
    user@host:~$ git checkout fido
    user@host:~$ cd ../../
    user@host:~$ nano out/current/build/conf/bblayers.conf
    /home/xe1gyq/Projects/edison-src/meta-intel-edison/meta-openembedded \
    user@host:~$ nano meta-intel-edison/meta-intel-edison-distro/recipes-core/images/edison-image.bb
    IMAGE_INSTALL += “opencv”
    PACKAGECONFIG_pn-opencv="eigen jpeg libav png tiff v4l”
    user@host:~$ cd out/current
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake edison-image

### Make Building Workflow

- meta-intel-edison/setup.sh
  - --dl_dir = bbcache/downloads
  - --sstate_dir = bbcache/sstate-cache
  - --build_dir = out/linux64 
  - --build_name = custom_build_xe1gyq@20151001233406
  - --sdk_host = linux64
- Repositories Cloning
  - poky-mirror.git
  - meta-mingw-mirror.git
  - meta-darwin-mirror.git
  - meta-intel-iot-middleware-mirror.git
  - poky
- Yocto Build Environment
  - build/conf/local.conf
  - source poky/oe-init-build-env
  - bitbake edison-image


    Build Configuration:
    BB_VERSION        = "1.24.0"
    BUILD_SYS         = "i686-linux"
    NATIVELSBSTRING   = "Debian-8.1"
    TARGET_SYS        = "i586-poky-linux"
    MACHINE           = "edison"
    DISTRO            = "poky-edison"
    DISTRO_VERSION    = "1.7.2"
    TUNE_FEATURES     = "m32 core2"
    TARGET_FPU        = ""
    meta              
    meta-yocto        
    meta-yocto-bsp    = "(detachedfromyocto-1.7.2):29812e61736a95f1de64b3e9ebbb9c646ebd28dd"
    meta-intel-edison-bsp 
    meta-intel-edison-distro = "<unknown>:<unknown>"
    meta-intel-iot-middleware = "(detachedfromc6d6814):c6d681475e76107e6c04c5f7a06034dc9e772d1e"
    meta-intel-arduino = "<unknown>:<unknown>"
    meta-arduino      = "1.6.x:541b127163acb243109f07141bf249da2ecdcd9a"

## Links

- [Intel® Edison Board Support Package](http://download.intel.com/support/edison/sb/edisonbsp_ug_331188007.pdf)

## Under investigation?
    
    - What is it create-debian-image.sh
    user@host:~$ edison-src/meta-intel-edison/utils

- https://software.intel.com/en-us/articles/opencv-300-beta-ipp-tbb-enabled-on-yocto-with-intel-edison
- http://download.intel.com/support/edison/sb/edisonbsp_ug_331188007.pdf
- https://hayestech.files.wordpress.com/2015/01/intel-edison-bsd.pdf
- http://www.instructables.com/id/Securing-IoT-applications-built-on-Intel-Galileo-a/
- http://www.embarcados.com.br/intel-edison-yocto-como-construir-sua-propria-distribuicao-linux-embarcado/
- http://www.embarcados.com.br/raspberry-pi-qt5-yocto-parte-1/
- https://communities.intel.com/docs/DOC-23391
- https://software.intel.com/en-us/articles/intel-edison-developer-resources
- http://download.intel.com/support/edison/sb/edisonbsp_ug_331188007.pdf
- http://drejkim.com/blog/2014/11/22/building-an-edison-image-and-changing-the-root-partition-size/
- https://hayestech.wordpress.com/2015/01/26/building-custom-intel-edison-images/
http://www.yoctoproject.org/docs/1.1/yocto-project-qs/yocto-project-qs.html
http://edplay.weebly.com/how-to/building-linux-for-intel-edison
- https://wiki.debian.org/EmDebian/CrossDebootstrap
- https://communities.intel.com/message/273743
- http://layers.openembedded.org/layerindex/branch/master/layer/meta-intel-edison-bsp/


    user@host:~$ tar xvf edison-src-weekly-68.tgz
    user@host:~$ ls edison-src
    arduino  broadcom_cws  device-software  mw
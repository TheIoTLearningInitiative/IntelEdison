Customization
==

Owner: Eduardo

## Dependencies

    user@host:~# sudo apt-get install build-essential git diffstat gawk chrpath texinfo libtool gcc-multilib dfu-util screen u-boot-tools

## Make

    user@host:~$ 
    user@host:~$ tar xvf edison-src-weekly-68b.tgz
    user@host:~$ cd edison-src
    user@host:~$ ls
    Makefile  meta-intel-edison
    user@host:~$ make setup
    user@host:~$ ls
    bbcache  Makefile  meta-arduino  meta-intel-edison  out  pub
    user@host:~$ cd out/linux64
    user@host:~$ ls
    build  poky
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake edison-image
    user@host:~$ ls
    arduino  bbcache  broadcom_cws  device-software  Makefile  meta-arduino meta-intel-edison  mw  out  pub
    user@host:~$ cd out/linux64/build/tmp/deploy/images/edison
    user@host:~$ cd meta-intel-edison/utils/flash
    user@host:~$ ls edison-src/build/tmp/deploy/images/edison/edison-image-edison.hddimg

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
    

## Script

    user@host:~$ tar xvf edison-src-weekly-68.tgz
    user@host:~$ ls edison-src
    arduino  broadcom_cws  device-software  mw
    user@host:~$ ./device-software/setup.sh
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ ../meta-intel-edison/utils/flash/postBuild.sh


- File name: edison-src-weekly-68.tgz @ https://downloadcenter.intel.com/download/24357
- https://scratchbuffer.wordpress.com/2015/09/01/yocto-linux-image-build-for-intel-edison-simple-and-easy/
- https://wiki.lsr.ei.tum.de/nst/documentation/inteledison

### Under investigation?
    
    - What is it create-debian-image.sh
    user@host:~$ edison-src/meta-intel-edison/utils

## Links 

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
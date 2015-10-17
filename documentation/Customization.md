Customization
==

Owner: Eduardo

## Dependencies

    user@host:~# sudo apt-get install build-essential git diffstat gawk chrpath texinfo libtool gcc-multilib dfu-util screen u-boot-tools

## Process Script

    user@host:~$ tar xvf edison-src-weekly-68.tgz
    user@host:~$ ls edison-src
    arduino  broadcom_cws  device-software  mw
    user@host:~$ ./device-software/setup.sh
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ ../meta-intel-edison/utils/flash/postBuild.sh


- File name: edison-src-weekly-68.tgz @ https://downloadcenter.intel.com/download/24357
- https://scratchbuffer.wordpress.com/2015/09/01/yocto-linux-image-build-for-intel-edison-simple-and-easy/
- https://wiki.lsr.ei.tum.de/nst/documentation/inteledison

## Process Make

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

### What is it create-debian-image.sh
    user@host:~$ edison-src/meta-intel-edison/utils

xe1gyq@jessie:~/Downloads/edison-src/out/linux64$ ls
build  poky

    xe1gyq@jessie:~/Downloads/edison-src$ ls
    arduino  bbcache  broadcom_cws  device-software  Makefile  meta-intel-edison  mw  out  pub


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
Customization
==

http://download.intel.com/support/edison/sb/edisonbsp_ug_331188007.pdf
https://hayestech.files.wordpress.com/2015/01/intel-edison-bsd.pdf

## Process A
https://downloadcenter.intel.com/download/24357
File name: edison-src-weekly-68.tgz

    xe1gyq@host:~$ tar xvf edison-src-weekly-68.tgz
    xe1gyq@host:~$ ls edison-src
    arduino  broadcom_cws  device-software  mw
    xe1gyq@host:~$ ./device-software/setup.sh
    xe1gyq@host:~$ source poky/oe-init-build-env
    xe1gyq@host:~$ ../meta-intel-edison/utils/flash/postBuild.sh

https://scratchbuffer.wordpress.com/2015/09/01/yocto-linux-image-build-for-intel-edison-simple-and-easy/
https://wiki.lsr.ei.tum.de/nst/documentation/inteledison

## Process B

http://www.embarcados.com.br/intel-edison-yocto-como-construir-sua-propria-distribuicao-linux-embarcado/

## Links 

- http://www.instructables.com/id/Securing-IoT-applications-built-on-Intel-Galileo-a/
- https://communities.intel.com/docs/DOC-23391
- https://software.intel.com/en-us/articles/intel-edison-developer-resources
- http://download.intel.com/support/edison/sb/edisonbsp_ug_331188007.pdf
- http://drejkim.com/blog/2014/11/22/building-an-edison-image-and-changing-the-root-partition-size/
- https://hayestech.wordpress.com/2015/01/26/building-custom-intel-edison-images/
http://www.yoctoproject.org/docs/1.1/yocto-project-qs/yocto-project-qs.html
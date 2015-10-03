Customization
==

http://download.intel.com/support/edison/sb/edisonbsp_ug_331188007.pdf
https://hayestech.files.wordpress.com/2015/01/intel-edison-bsd.pdf

## Process A
https://downloadcenter.intel.com/download/24357
File name: edison-src-weekly-68.tgz

    xe1gyq@host:~# sudo apt-get install build-essential git diffstat gawk chrpath texinfo libtool gcc-multilib dfu-util screen u-boot-tools

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
http://www.embarcados.com.br/raspberry-pi-qt5-yocto-parte-1/

    user@host:~$ 
    user@host:~$ tar xvf edison-src-weekly-68b.tgz
    user@host:~$ cd edison-src
    user@host:~$ make setup
    user@host:~$ cd out/linux64
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake edison-image
    user@host:~$ cd edison-src/out/linux64/build/tmp/deploy/images/edison

    user@host:~$ cd edison-src/meta-intel-edison/utils/flash
    
    edison-src/build/tmp/deploy/images/edison/edison-image-edison.hddimg

### What is it create-debian-image.sh
    user@host:~$ edison-src/meta-intel-edison/utils


xe1gyq@jessie:~/Downloads/edison-src$ ls
arduino  bbcache  broadcom_cws  device-software  Makefile  meta-arduino  meta-intel-edison  mw  out  pub

xe1gyq@jessie:~/Downloads/edison-src/out/linux64$ ls
build  poky

xe1gyq@jessie:~/Downloads/edison-src$ ls
arduino  bbcache  broadcom_cws  device-software  Makefile  meta-intel-edison  mw  out  pub
xe1gyq@jessie:~/Downloads/edison-src$ make
Please run "make setup" first
Makefile:106: recipe for target '_check_setup_was_done' failed
make: *** [_check_setup_was_done] Error 1
xe1gyq@jessie:~/Downloads/edison-src$ make setup
Setup buildenv for SDK host linux64
./meta-intel-edison/setup.sh  --dl_dir=/home/xe1gyq/Downloads/edison-src/bbcache/downloads --sstate_dir=/home/xe1gyq/Downloads/edison-src/bbcache/sstate-cache --build_dir=/home/xe1gyq/Downloads/edison-src/out/linux64 --build_name=custom_build_xe1gyq@20151001233406 --sdk_host=linux64
We are building in external mode
Cloning into bare repository 'poky-mirror.git'...
remote: Counting objects: 288590, done.
remote: Compressing objects: 100% (71063/71063), done.
remote: Total 288590 (delta 212301), reused 288186 (delta 211897)
Receiving objects: 100% (288590/288590), 114.57 MiB | 581.00 KiB/s, done.
Resolving deltas: 100% (212301/212301), done.
Checking connectivity... done.
Cloning into bare repository 'meta-mingw-mirror.git'...
remote: Counting objects: 256, done.
remote: Compressing objects: 100% (191/191), done.
remote: Total 256 (delta 98), reused 203 (delta 45)
Receiving objects: 100% (256/256), 62.01 KiB | 0 bytes/s, done.
Resolving deltas: 100% (98/98), done.
Checking connectivity... done.
Cloning into bare repository 'meta-darwin-mirror.git'...
remote: Counting objects: 577, done.
remote: Compressing objects: 100% (329/329), done.
remote: Total 577 (delta 244), reused 522 (delta 189)
Receiving objects: 100% (577/577), 6.90 MiB | 606.00 KiB/s, done.
Resolving deltas: 100% (244/244), done.
Checking connectivity... done.
Cloning into bare repository 'meta-intel-iot-middleware-mirror.git'...
remote: Counting objects: 1008, done.
remote: Compressing objects: 100% (534/534), done.
remote: Total 1008 (delta 506), reused 880 (delta 380)
Receiving objects: 100% (1008/1008), 5.60 MiB | 603.00 KiB/s, done.
Resolving deltas: 100% (506/506), done.
Checking connectivity... done.
Cloning Poky in the /home/xe1gyq/Downloads/edison-src/out/linux64/poky directory
Cloning into 'poky'...
done.
Checking out files: 100% (5016/5016), done.
Note: checking out 'yocto-1.7.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b new_branch_name

HEAD is now at 29812e6... busybox: unbreak tar of uncompressed files
Cloning Mingw layer to /home/xe1gyq/Downloads/edison-src/out/linux64/poky/meta-mingw directory from local cache
Cloning into 'meta-mingw'...
done.
Cloning Darwin layer to /home/xe1gyq/Downloads/edison-src/out/linux64/poky/meta-darwin directory from local cache
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
Cloning meta-intel-iot-middleware layer to /home/xe1gyq/Downloads/edison-src/out/linux64/poky/meta-intel-iot-middleware directory from local cache
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
Cloning meta-arduino layer to /home/xe1gyq/Downloads/edison-src directory from GitHub.com/01org/meta-arduino
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
cd /home/xe1gyq/Downloads/edison-src/out/linux64
source poky/oe-init-build-env
bitbake edison-image
*************
xe1gyq@jessie:~/Downloads/edison-src$ cd /home/xe1gyq/Downloads/edison-src/out/linux64
xe1gyq@jessie:~/Downloads/edison-src/out/linux64$ source poky/oe-init-build-env

### Shell environment set up for builds. ###

You can now run 'bitbake <target>'

Common targets are:
    core-image-minimal
    core-image-sato
    meta-toolchain
    adt-installer
    meta-ide-support

You can also run generated qemu images with a command like 'runqemu qemux86'
xe1gyq@jessie:~/Downloads/edison-src/out/linux64/build$ bitbake edison-image
WARNING: Host distribution "Debian-8.1" has not been validated with this version of the build system; you may possibly experience unexpected failures. It is recommended that you use a tested distribution.
Parsing recipes: 100% |###################################################################################| Time: 00:02:01
Parsing of 959 .bb files complete (0 cached, 959 parsed). 1364 targets, 117 skipped, 0 masked, 0 errors.
NOTE: Resolving any missing task queue dependencies

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

NOTE: Preparing runqueue
NOTE: Executing SetScene Tasks
NOTE: Executing RunQueue Tasks
WARNING: Failed to fetch URL http://zlib.net/pigz/pigz-2.3.1.tar.gz, attempting MIRRORS if available
WARNING: Failed to fetch URL ftp://ftp.debian.org/debian/pool/main/b/base-passwd/base-passwd_3.5.29.tar.gz, attempting MIRRORS if available
WARNING: Failed to fetch URL http://downloads.sourceforge.net/project/libpng/libpng16/1.6.13/libpng-1.6.13.tar.xz, attempting MIRRORS if available
NOTE: validating kernel config, see log.do_kernel_configcheck for details
WARNING: Failed to fetch URL http://www.apache.org/dist/apr/apr-1.5.1.tar.bz2, attempting MIRRORS if available
WARNING: Failed to fetch URL http://www.apache.org/dist/apr/apr-util-1.5.3.tar.gz, attempting MIRRORS if available
WARNING: QA Issue: bluez5: configure was passed unrecognised options: --with-systemdunitdir [unknown-configure-option]
WARNING: Failed to fetch URL http://www.apache.org/dist/subversion/subversion-1.8.9.tar.bz2, attempting MIRRORS if available
WARNING: Failed to fetch URL ftp://ftp.debian.org/debian/pool/main/n/netbase/netbase_5.2.tar.gz, attempting MIRRORS if available
WARNING: Failed to fetch URL ftp://ftp.uni-erlangen.de/pub/Linux/LOCAL/dosfstools/dosfstools-2.11.src.tar.gz, attempting MIRRORS if available
WARNING: busybox: alternative target (/etc/syslog.conf or /etc/syslog.conf.busybox) does not exist, skipping...
WARNING: busybox: NOT adding alternative provide /etc/syslog.conf: /etc/syslog.conf.busybox does not exist
WARNING: alt_link == alt_target: /etc/syslog.conf == /etc/syslog.conf
WARNING: Failed to fetch URL ftp://ftp.debian.org/debian/pool/main/n/net-tools/net-tools_1.60-25.diff.gz;apply=no;name=patch, attempting MIRRORS if available
WARNING: Failed to fetch URL http://dl.lm-sensors.org/i2c-tools/releases/i2c-tools-3.1.1.tar.bz2, attempting MIRRORS if available
WARNING: Failed to fetch URL ftp://lsof.itap.purdue.edu/pub/tools/unix/lsof/lsof_4.87.tar.bz2, attempting MIRRORS if available
WARNING: Failed to fetch URL ftp://ftp.debian.org/debian/pool/main/d/dpkg/dpkg_1.17.4.tar.xz, attempting MIRRORS if available
WARNING: Failed to fetch URL http://ftp.de.debian.org/debian/pool/main/m/mklibs/mklibs_0.1.39.tar.xz, attempting MIRRORS if available
WARNING: Failed to fetch URL ftp://ftp.berlios.de/pub/cdrecord/alpha/cdrtools-3.01a20.tar.bz2, attempting MIRRORS if available
WARNING: QA Issue: battery-voltage rdepends on libsystemd, but it isn't a build dependency? [build-deps]
WARNING: QA Issue: xdk-daemon requires libdns_sd.so, but no providers in its RDEPENDS [file-rdeps]
WARNING: QA Issue: iotkit-agent requires /bin/bash, but no providers in its RDEPENDS [file-rdeps]
WARNING: QA Issue: pulseaudio-module-console-kit rdepends on consolekit, but it isn't a build dependency? [build-deps]
WARNING: QA Issue: post-install requires /bin/bash, but no providers in its RDEPENDS [file-rdeps]
WARNING: QA Issue: systemd-kernel-install requires /bin/bash, but no providers in its RDEPENDS [file-rdeps]
WARNING: QA Issue: wpa-supplicant-passphrase rdepends on libcrypto, but it isn't a build dependency? [build-deps]
WARNING: QA Issue: wpa-supplicant rdepends on libcrypto, but it isn't a build dependency? [build-deps]
WARNING: QA Issue: wpa-supplicant rdepends on libssl, but it isn't a build dependency? [build-deps]
NOTE: Tasks Summary: Attempted 3757 tasks of which 13 didn't need to be rerun and all succeeded.

Summary: There were 28 WARNING messages shown.

## Links 

- http://www.instructables.com/id/Securing-IoT-applications-built-on-Intel-Galileo-a/
- https://communities.intel.com/docs/DOC-23391
- https://software.intel.com/en-us/articles/intel-edison-developer-resources
- http://download.intel.com/support/edison/sb/edisonbsp_ug_331188007.pdf
- http://drejkim.com/blog/2014/11/22/building-an-edison-image-and-changing-the-root-partition-size/
- https://hayestech.wordpress.com/2015/01/26/building-custom-intel-edison-images/
http://www.yoctoproject.org/docs/1.1/yocto-project-qs/yocto-project-qs.html
http://edplay.weebly.com/how-to/building-linux-for-intel-edison
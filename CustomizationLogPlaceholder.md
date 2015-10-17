# Customization Log Placeholder

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
    ...
    NOTE: Tasks Summary: Attempted 3757 tasks of which 13 didn't need to be rerun and all succeeded.

    Summary: There were 28 WARNING messages shown.
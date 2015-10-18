Linux Kernel
==

## Building via Make

    user@host:~$ pwd
    /home/xe1gyq/Projects/edison-src
    user@host:~$ cd out/current
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake virtual/kernel -c menuconfig
    ...
    edison-src/out/linux64/build/tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/Makefile
    ...
    user@host:~$ cp tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/.config tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/defconfig 
    user@host:~$ cp tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/.config tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux/arch/x86/configs/i386_edison_defconfig
    user@host:~$ bitbake virtual/kernel -c configure -f -v
    user@host:~$ cd ../../..
    user@host:~$ make image
    user@host:~$ make flash
    edison-src/out/linux64/build/tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/Makefile

Kernel Macros

    CONFIG_BMP085=y
    CONFIG_BMP085_I2C=y
    
## Building via BitBake (Unchecked)

    user@host:~$ pwd
    /home/xe1gyq/Projects/edison-src
    user@host:~$ cd out/current
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ bitbake virtual/kernel -c menuconfig
    ...
    edison-src/out/linux64/build/tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/Makefile
    ...
    user@host:~$ cp tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/.config tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/defconfig 
    user@host:~$ cp tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux-edison-standard-build/.config tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux/arch/x86/configs/i386_edison_defconfig
    user@host:~$ bitbake virtual/kernel -c configure -f -v
    user@host:~$ bitbake edison-image

## Hello World Kernel Module

    user@host:~$ pwd
    /home/xe1gyq/Projects/edison-src
    user@host:~$ cd out/current
    user@host:~$ source poky/oe-init-build-env
    user@host:~$ pwd
    ...
    user@host:~$ cd tmp/work/edison-poky-linux/linux-yocto/3.10.17-r0/linux/
    user@host:~$ mkdir drivers/helloworld
    user@host:~$ nano drivers/helloworld/helloworld.c


```C
#include <linux/init.h>
#include <linux/kernel.h>
#include <linux/module.h>

static int module_init_function(void)
{
    printk(KERN_INFO "Module? Hello!\n");
    return 0;
}

static void module_exit_function(void)
{
    printk(KERN_INFO "Module? Bye!\n");
}

MODULE_LICENSE("GPL");
MODULE_AUTHOR("xe1gyq");
MODULE_DESCRIPTION("My First Linux Kernel Module");

module_init(module_init_function);
module_exit(module_exit_function);
```

    user@host:~$ nano drivers/helloworld/Kconfig

```
    menu "Hello Module Kernel Support"
    config HELLO_WORLD
            tristate "Hello Module Driver"
            depends on X86
            help
              Select this option to run a Hello World Module!
    endmenu
```

    user@host:~$ nano drivers/helloworld/Makefile
    obj-$(CONFIG_HELLO_WORLD)               += helloworld.o
    user@host:~$ nano drivers/Kconfig
    menu "Device Drivers"
    source "drivers/helloworld/Kconfig"
    source "drivers/amba/Kconfig"
    ...
    user@host:~$ nano drivers/Makefile

```
    ...
    # Rewritten to use lists instead of if-statements.
    #
    obj-$(CONFIG_HELLO_WORLD) += helloworld/
    obj-y += irqchip/
    ...
```
    user@host:~$ bitbake virtual/kernel -c menuconfig
    user@host:~$ 
    user@host:~$ 
    user@host:~$ 
    
## Others

    user@host:~$ nano edison-src/meta-intel-edison/meta-intel-edison-bsp/recipes-kernel/linux/files/defconfig
    user@host:~$ nano edison-src/meta-intel-edison/meta-intel-edison-bsp/recipes-kernel/linux/files/upstream_to_edison.patch
    user@host:~$ find -name 
    user@host:~$ cp /build/tmp/work/edison-poky-linux/linuxyocto/3.10.17+gitAUTOINC+6ad20f049a_c03195ed6e-r0/linux-edison-standardbuild/.config build/tmp/work/edison-poky-linux/linuxyocto/3.10.17+gitAUTOINC+6ad20f049a_c03195ed6er0/defconfig

## Links

- [Yocto Project Linux Kernel Development Manual](http://www.yoctoproject.org/docs/latest/kernel-dev/kernel-dev.html)

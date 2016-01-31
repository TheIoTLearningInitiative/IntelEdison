Yocto Customization
==

> The Yocto Project is a Linux Foundation workgroup whose goal is to produce tools and processes that will enable the creation of Linux distributions for embedded software that are independent of the underlying architecture of the embedded software itself.

- [Yocto Project Homepage](https://www.yoctoproject.org/)
- [Yocto Project and Embedded OS Webinar](http://www.intel.com/content/www/us/en/education/university/galileo-university-curricula/yocto-project-and-embedded-os-webinar-replay.html#)

## Building Yocto

Let's understand what it means to work with Yocto Project by building images for QEMU and Minnowboard MAX.

### Development Workstation, Qemu Image Compilaton

```sh
    user@host:~# apt-get install gawk wget git-core diffstat unzip texinfo build-essential chrpath
    user@host:~# apt-get install qemu
    user@host:~$ mkdir source
    user@host:~$ cd source
    user@host:~$ git clone git://git.yoctoproject.org/poky --branch fido
    user@host:~$ source poky/oe-init-build-env yocto-x86-minimal
    user@host:~$ bitbake core-image-minimal
    user@host:~$ bitbake core-image-full-cmdline-x86
    user@host:~$ bitbake core-image-sato-sdk
    user@host:~$ runqemu qemux86
```

## Links

- [Code Project Adding 3rd Party Components to Yocto/OpenEmbedded Linux](http://www.codeproject.com/Articles/774826/Adding-rd-party-components-to-Yocto-OpenEmbedded-L)
 
## SandBox

ToDo Important Topics To Cover

- Example Project
- Adding Recipes to the Build System
- Adding New Recipes to the Build System
- Build an Example Package based on a Git Repository Commit
- Build an example package based on a Remote Source Archive
- Build an example package based on a Local Source Archive

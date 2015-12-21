Building Blocks
==

    BBLAYERS ?= " \
      /home/abraham/Projects/RealTime/v25/edison-src/out/linux64/poky/meta \
      /home/abraham/Projects/RealTime/v25/edison-src/out/linux64/poky/meta-yocto \
      /home/abraham/Projects/RealTime/v25/edison-src/out/linux64/poky/meta-yocto-bsp \
      /home/abraham/Projects/RealTime/v25/edison-src/meta-intel-edison/meta-intel-edison-bsp \
      /home/abraham/Projects/RealTime/v25/edison-src/meta-intel-edison/meta-intel-edison-distro \
      /home/abraham/Projects/RealTime/v25/edison-src/out/linux64/poky/meta-intel-iot-middleware \
      /home/abraham/Projects/RealTime/v25/edison-src/meta-intel-edison/meta-intel-arduino \
      /home/abraham/Projects/RealTime/v25/edison-src/meta-arduino \
      \
      "
    BBLAYERS_NON_REMOVABLE ?= " \
      /home/abraham/Projects/RealTime/v25/edison-src/out/linux64/poky/meta \
      /home/abraham/Projects/RealTime/v25/edison-src/out/linux64/poky/meta-yocto \
      "



### poky/meta

> Yocto Metadata Layers

    recipes-bsp          - Anything with links to specific hardware or hardware configuration information
    recipes-connectivity - Libraries and applications related to communication with other devices
    recipes-core         - What's needed to build a basic working Linux image including commonly used dependencies
    recipes-devtools     - Tools primarily used by the build system (but can also be used on targets)
    recipes-extended     - Applications which whilst not essential add features compared to the alternatives in
                           core. May be needed for full tool functionality or LSB compliance.
    recipes-gnome        - All things related to the GTK+ application framework
    recipes-graphics     - X and other graphically related system libraries
    recipes-kernel       - The kernel and generic applications/libraries with strong kernel dependencies
    recipes-lsb4         - Recipes added for the sole purpose of supporting the Linux Standard Base (LSB) 4.x
    recipes-multimedia   - Codecs and support utilties for audio, images and video
    recipes-rt           - Provides package and image recipes for using and testing the PREEMPT_RT kernel
    recipes-qt           - All things related to the Qt application framework
    recipes-sato         - The Sato demo/reference UI/UX, its associated apps and configuration
    recipes-support      - Recipes used by other recipes but that are not directly included in images

### meta-yocto

> Yocto Project integration layers (Poky distro configuration, reference hardware BSPs) 

[Yocto meta-yocto](http://git.yoctoproject.org/cgit/cgit.cgi/meta-yocto)
[OpenEmbedded meta-yocto](http://layers.openembedded.org/layerindex/branch/master/layer/meta-yocto/)

### meta-yocto-bsp 

> BSP layer for Yocto Project reference hardware


## Links

- [Layer for the Intel Edison Development Platform](http://git.yoctoproject.org/cgit/cgit.cgi/meta-intel-edison/tree/)
- [Intel Galileo platform support](http://git.yoctoproject.org/cgit/cgit.cgi/meta-intel-galileo/tree/)
- [Intel Galileo Rebuild](http://www.embarcados.com.br/galileo-yocto/)

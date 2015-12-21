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



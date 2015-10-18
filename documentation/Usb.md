USB
==

## Kernel Integration


## Userspace Applications

    root@edison:~# dmesg
    root@edison:~# lsusb
    unable to initialize libusb: -99

## Setup
### Opkg

    root@Edison:~# opkg install libusb-1.0-dev libudev1-dev

### Apt-Get

    root@Edison:~# apt-get install libusb-1.0-dev libudev-dev
    root@Edison:~# libtool
    
    root@Edison:~# git clone https://github.com/libusb/libusb.git
    root@Edison:~# cd libusb
    root@Edison:~# ./autogen.sh -disable-udev
    root@Edison:~# make
    root@Edison:~# cd examples
    root@Edison:~# ./listdevs
    1d6b:0003 (bus 2, device 1)
    0458:708a (bus 1, device 3) path: 1.1
    05e3:0606 (bus 1, device 2) path: 1
    1d6b:0002 (bus 1, device 1)

## Device Configuration

    root@edison:~# lsmod | grep uvc
    root@edison:~# ls -al /dev/video0

## Usage Models


## Links

- http://www.yoctopuce.com/
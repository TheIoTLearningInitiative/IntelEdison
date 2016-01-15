USB
==

> libusb is a C library that gives applications easy access to USB devices on many different operating systems.

- [libusb homepage](http://www.libusb.org/)

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
    root@Edison:~# apt-get install libtool
    
## Device Configuration

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

## Usage Models

## Debug

    $ dmesg
    root@Edison:~# ls -l /sys/bus/usb/drivers
    total 0
    drwxr-xr-x 2 root root 0 Jan  1 00:01 asix
    drwxr-xr-x 2 root root 0 Jan  1 00:01 cdc_acm
    drwxr-xr-x 2 root root 0 Jan  1 00:01 cdc_ncm
    drwxr-xr-x 2 root root 0 Jan  1 00:01 cdc_subset
    drwxr-xr-x 2 root root 0 Jan  1 00:01 ftdi_sio
    drwxr-xr-x 2 root root 0 Jan  1 00:01 hub
    drwxr-xr-x 2 root root 0 Jan  1 00:01 pl2303
    drwxr-xr-x 2 root root 0 Jan  1 00:01 snd-usb-audio
    drwxr-xr-x 2 root root 0 Jan  1 00:01 usb
    drwxr-xr-x 2 root root 0 Jan  1 00:01 usbfs
    drwxr-xr-x 2 root root 0 Jan  1 00:01 usbhid
    drwxr-xr-x 2 root root 0 Jan  1 00:01 usbserial
    drwxr-xr-x 2 root root 0 Jan  1 00:01 usb-storage
    drwxr-xr-x 2 root root 0 Jan  1 00:01 uvcvideo
    root@Edison:~# ls –l /sys/bus/usb/drivers/option/***/
    $ cat /sys/bus/usb/drivers/option/***/bInterface*
    $ cat /proc/bus/usb/devices

## Links

- http://www.yoctopuce.com/
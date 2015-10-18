USB
==

## Userspace Applications

    root@edison:~# lsusb
    root@edison:~# dmesg
    root@edison:~/libusb# lsusb
    unable to initialize libusb: -99

## Setup
### Opkg

    root@Edison:~# opkg install libusb-1.0-dev libudev1-dev

### Apt-Get

    root@Edison:~# apt-get install libusb-1.0-dev libudev1-dev

## Links

- http://www.yoctopuce.com/
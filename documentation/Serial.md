Serial
==

## Kernel Integration

    root@edison:~# dmesg | grep -i serial
    root@edison:~# dmesg | grep -i tty
    root@edison:~# find /sys/ -name 'tty:ttyS*'
    root@edison:~# lspci
    root@edison:~# ls /dev/tty*
    root@edison:~# setserial -g /dev/ttyS[0123]

## Userspace Applications

    root@edison:~# minicom /dev/ttyS0
    root@edison:~# minicom /dev/ttyUSB0

## Setup
### Apt-Get
### Opkg
## Device Configuration
## Usage Models

    import serial
    ser = serial.Serial("/dev/ttyACM0", timeout=10)
    lines = ser.readlines()
    for i in range(10):
    print(lines[i].strip())

## Links

- https://communities.intel.com/thread/54236
- [Sparkfun Serial Terminal Basics](https://learn.sparkfun.com/tutorials/terminal-basics/all)

Serial
==

## Kernel Integration

    root@edison:~# find /sys/ -name 'tty:ttyS*'
    root@edison:~# lspci
    root@edison:~# ls /dev/tty*

## Userspace Applications

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

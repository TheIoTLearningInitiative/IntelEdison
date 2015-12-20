Serial
==

## Userspace Required Applications

    root@edison:~# echo screen minicom

## Kernel Display Message

    root@edison:~# dmesg | grep -i serial
    root@edison:~# dmesg | grep -i tty
    root@edison:~# find /sys/ -name 'tty:ttyS*'
    root@edison:~# lspci
    root@edison:~# ls /dev/tty*
    root@edison:~# setserial -g /dev/ttyS[0123]
    root@edison:~# setserial -g /dev/ttyUSB[0123]

## Userspace Applications

    root@edison:~# screen /dev/ttyS0
    root@edison:~# minicom /dev/ttyS0
    root@edison:~# cu /dev/ttyUSB0 115200
    root@edison:~# setserial -g /dev/ttyS[0123]
    root@edison:~# setserial -g /dev/ttyUSBS[0123]

## Device Configuration

    root@edison:~# setserial /dev/ttyS0 115200
    root@edison:~# stty -F /dev/ttyUSB0 115200 

## Usage Models

```python
import serial
ser = serial.Serial("/dev/ttyACM0", timeout=10)
lines = ser.readlines()
    for i in range(10):
print(lines[i].strip())
```

## Links

- [Intel Edison Types of Serial Ports](https://communities.intel.com/thread/54236)
- [Sparkfun Serial Terminal Basics](https://learn.sparkfun.com/tutorials/terminal-basics/all)
- [TLDP Serial HOWTO](http://www.tldp.org/HOWTO/Serial-HOWTO.html)

Serial
==

## Kernel Integration
## Userspace Applications

    root@edison:~# ls /dev/tty*
    root@edison:~# find /sys/ -name 'tty:ttyS*'

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

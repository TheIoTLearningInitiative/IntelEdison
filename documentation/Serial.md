Serial
==

    import serial
    ser = serial.Serial("/dev/ttyACM0", timeout=10)
    lines = ser.readlines()
    for i in range(10):
    print(lines[i].strip())

## Links

- https://communities.intel.com/thread/54236

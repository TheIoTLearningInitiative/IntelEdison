BlueTooth
==

> Bluetooth is a wireless technology standard for exchanging data over short distances (using short-wavelength UHF radio waves in the ISM band from 2.4 to 2.485 GHz[4]) from fixed and mobile devices, and building personal area networks (PANs). Wikipedia

- [Bluetooth Wikipedia](https://en.wikipedia.org/wiki/Bluetooth)
- [Intel® Edison Bluetooth Guide](http://download.intel.com/support/edison/sb/edisonbluetooth_331704004.pdf)

## Required Applications

### Opkg

    root@edison:~# opkg install bluez5-dev
    root@edison:~# pip install bluez5

### Apt-Get

    root@edison:~# apt-get install bluetooth
    root@edison:~# /etc/init.d/bluetooth start

## Kernel Display Message

    root@edison:~# dmesg | grep -i blue
    [    0.235619] Bluetooth: Core ver 2.16
    [    0.235722] Bluetooth: HCI device and connection manager initialized
    [    0.235752] Bluetooth: HCI socket layer initialized
    [    0.235778] Bluetooth: L2CAP socket layer initialized
    [    0.235876] Bluetooth: SCO socket layer initialized
    [    0.922994] Bluetooth: HCI UART driver ver 2.2
    [    0.923015] Bluetooth: HCI H4 protocol initialized
    [    1.588016] Bluetooth: RFCOMM TTY layer initialized
    [    1.588081] Bluetooth: RFCOMM socket layer initialized
    [    1.588100] Bluetooth: RFCOMM ver 1.11
    [    1.588116] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
    [    1.588130] Bluetooth: BNEP filters: protocol multicast
    [    1.588160] Bluetooth: BNEP socket layer initialized
    [    1.588175] Bluetooth: HIDP (Human Interface Emulation) ver 1.2
    [    1.588202] Bluetooth: HIDP socket layer initialized
    root@edison:/tmp# lsmod
    Module                  Size  Used by
    usb_f_acm              14335  1 
    ...
    bcm_bt_lpm             13708  0 

    bcm4334x              587105  0 

## Userspace Applications

- bluetooth-agent
- bluetoothctl
- hciconfig
- hcitool


    root@edison:~# systemctl status bluetooth.service
    root@edison:~# systemctl stop bluetooth
    root@edison:~# systemctl start bluetooth
    root@edison:~# systemctl enable bluetooth
    root@edison:~# rfkill unblock bluetooth
    root@edison:~# rfkill list bluetooth
    2: bcm43xx Bluetooth: bluetooth
    ...
    3: hci0: bluetooth
    ...
    root@edison:~# hciconfig hci0 down
    root@edison:~# hciconfig hci0 up
    root@edison:~# hciconfig hci0 status
    hci0:   Type: BR/EDR  Bus: UART
        BD Address: 98:4F:EE:03:39:02  ACL MTU: 1021:8  SCO MTU: 64:1
        UP RUNNING PSCAN 
    ...
    root@edison:~# hciconfig hci0 piscan
    ...
    root@edison:~# hcitool scan

## Usage Models

### Device Pairing

    root@galileo:~# rfkill unblock bluetooth
    root@galileo:~# bluetoothctl
    [bluetooth]# scan on
    [bluetooth]# scan off
    [bluetooth]# pair 40:78:6A:26:4A:C2
    [bluetooth]# connect 40:78:6A:26:4A:C2
    [bluetooth]# paired-devices
    [bluetooth]# info 40:78:6A:26:4A:C2
    [bluetooth]# exit

### Text

    root@edison:~# systemctl status bluetooth.service
    root@edison:~# systemctl start bluetooth
    root@edison:~# systemctl enable bluetooth
    root@edison:~# rfkill unblock bluetooth
    root@edison:~# rfkill list bluetooth
    root@edison:~# hciconfig hci0 status
    Make Your Device Discoverable
    root@edison:~# hcitool scan
    root@edison:~# rfcomm bind 0 40:78:6A:26:4A:C2
    

### Audio

    root@edison:~# apt-get install pulseaudio pulseaudio-module-bluetooth pavucontrol bluez-firmware

### Serial Port Profile (SPP)

Libraries

For c bluetooth development:

    root@edison:~# sudo apt-get install libbluetooth-dev

For python bluetooth development:

    root@edison:~# sudo apt-get install python-bluez
    
For python bluetooth in Edison (using pip, if for some reason you don't have it, learn [How-To install pip](https://pip.pypa.io/en/stable/installing/#pip-included-with-python)):

    root@edison:~# pip install pybluez

There are two common ways to test SPP, one is by using D-BUS, the other is by using RFCOMM transport protocol.

To test using D-Bus we can use [this python script](http://downloadmirror.intel.com/24909/eng/SPP-loopback.py), copy it to Edison, enable the bluetooth device and run it:

    root@edison:~# rfkill unblock bluetooth
    root@edison:~# python SPP-loopback.py &

then in an android device install a [Bluetooth SPP Manager](https://play.google.com/store/apps/details?id=at.rtcmanager).

At this point you need to pair the Edison with your android device (see example above on how to use **bluetoothctl**, **hcicontrol** or any other user level application in your Edison).

Once paired, open the Bluetooth SPP Manager app, hit seach, and when the edison appears  tap on in to connect.  now you can send text messages to Edison which can be seen on the terminal window of the Edison.

--

I know this need a lil' bit further explanation. just dropped here so i won't forget

also what is going to be added is  how to  programmatically do the device discovering, pairing  and SPP using c and python

--

## Links

- [Intel® Edison Boards Bluetooth® User Guide](http://www.intel.com/support/edison/sb/CS-035381.htm)
- http://alextgalileo.altervista.org/blog/install-kernel-from-repo-onto-edison-official-image/
- https://software.intel.com/en-us/articles/intel-edison-board-getting-started-with-bluetooth
- http://rexstjohn.com/lets-turn-intel-edison-into-an-ibeacon/
- http://unix.stackexchange.com/questions/53546/debian-squeeze-connect-to-a2dp-bluetooth-through-command-line
- https://software.intel.com/en-us/articles/using-the-generic-attribute-profile-gatt-in-bluetooth-low-energy-with-your-intel-edison
- https://software.intel.com/en-us/articles/connecting-the-intel-edison-board-to-your-android-phone-with-serial-port-profile-spp
- [Profiles](https://downloadmirror.intel.com/24909/eng/edison-bsp_rn_332032-007.pdf)
- https://learn.sparkfun.com/tutorials/bluetooth-basics
- [PyBluez API Ddoc](http://pybluez.googlecode.com/svn/www/docs-0.7/index.html)
- [PIP package manager](https://pip.pypa.io/en/stable/)

## SandBox

- Intel® Edison to a Bluetooth Network
- Intel® Edison from a peer device 

    root@edison:~# rfcomm bind - 40:78:6A:26:4A:C2 1
    root@edison:~# ls /dev/rfcomm0
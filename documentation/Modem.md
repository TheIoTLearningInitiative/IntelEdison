# Modem


    root@ubilinux:~# apt-get update
    root@ubilinux:~# apt-get install ppp
    root@ubilinux:~# wget "http://www.sakis3g.com/downloads/sakis3g.tar.gz" -O sakis3g.tar.gz
    root@ubilinux:~# tar -xzvf sakis3g.tar.gz
    root@ubilinux:~# chmod +x sakis3g
    root@ubilinux:~# ./sakis3g --interactive

    root@ubilinux:~# dmesg
    [  450.792009] usb 1-1.3: new high-speed USB device number 3 using dwc3-host
    [  450.817656] usb 1-1.3: New USB device found, idVendor=1bbb, idProduct=f017
    [  450.817688] usb 1-1.3: New USB device strings: Mfr=3, Product=2, SerialNumber=0
    [  450.817709] usb 1-1.3: Product: Mobile Broad Band
    [  450.817727] usb 1-1.3: Manufacturer: USBModem
    [  450.821346] usb-storage 1-1.3:1.0: USB Mass Storage device detected
    [  450.821851] scsi0 : usb-storage 1-1.3:1.0
    [  450.822947] usb-storage 1-1.3:1.1: USB Mass Storage device detected
    [  450.823370] scsi1 : usb-storage 1-1.3:1.1
    [  451.823343] scsi 0:0:0:0: Direct-Access     USBModem MMC Storage      2.31 PQ: 0 ANSI: 2
    [  451.824283] scsi 1:0:0:0: CD-ROM            USBModem MMC Storage      2.31 PQ: 0 ANSI: 2
    [  451.827155] sd 0:0:0:0: Attached scsi generic sg0 type 0
    [  451.828944] sr0: scsi-1 drive
    [  451.828967] cdrom: Uniform CD-ROM driver Revision: 3.20
    [  451.830033] sr 1:0:0:0: Attached scsi CD-ROM sr0
    [  451.830818] sr 1:0:0:0: Attached scsi generic sg1 type 5
    [  451.831854] sd 0:0:0:0: [sda] Attached SCSI removable disk
    root@ubilinux:~# lsusb
    Bus 001 Device 002: ID 8564:4000  
    Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
    Bus 001 Device 003: ID 1bbb:f017 T & A Mobile Phones
    
    

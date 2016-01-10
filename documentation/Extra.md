Extra
==

Setup

- Configure Wireless LAN


    apt-get update
    apt-get install git
    apt-get usb-modeswitch
    apt-get install build-essential g++ automake autoconf gnu-standards autoconf-doc libtool gettext autoconf-archive
    apt-get install wvdial
    apt-get install bzip2

## Squid Proxy

> Squid is a caching proxy for the Web supporting HTTP, HTTPS, FTP, and more. It reduces bandwidth and improves response times by caching and reusing frequently-requested web pages. Squid has extensive access controls and makes a great server accelerator. It runs on most available operating systems, including Windows and is licensed under the GNU GPL.


    apt-get install squid3 squid3-common


- http://linuxaria.com/pills/how-to-setup-a-squid-proxy-on-your-debian-linux

## DHCP


    apt-get install dhcpd


## Apache


    apt-get install apache2
    apache2 -k restart # Wrong
    /etc/init.d/apache2 restart # Ok


## WifiDog

    root@ubilinux:~/wifidog-gateway# git clone https://github.com/wifidog/wifidog-gateway.git
    root@ubilinux:~/wifidog-gateway# ./autogen.sh
    root@ubilinux:~/wifidog-gateway# ./configure
    root@ubilinux:~/wifidog-gateway# make
    root@ubilinux:~/wifidog-gateway# make install
    root@ubilinux:~/wifidog-gateway# wifidog 
    [6][Fri Jan  8 23:23:20 2016][16159](conf.c:651) Reading configuration file '/usr/local/etc/wifidog.conf'
    [3][Fri Jan  8 23:23:20 2016][16159](conf.c:654) Could not open configuration file '/usr/local/etc/wifidog.conf', exiting...

    root@ubilinux:~# git clone https://github.com/wifidog/wifidog-auth.git
    
    root@ubilinux:~# apt-get install postgresql-9.1
    root@ubilinux:~# apt-get install php5-pgsql
    root@ubilinux:~# apt-get install php-pear
    root@ubilinux:~# apt-get install php5-curl
    root@ubilinux:~# wget http://prdownloads.sourceforge.net/phlickr/Phlickr-0.2.5.tgz?download
    root@ubilinux:~# pear install Phlickr-0.2.5.tgz\?download
    root@ubilinux:~# 
    root@ubilinux:~# 
    root@ubilinux:~# 

    
### Links

- https://github.com/wifidog/wifidog-auth/blob/master/INSTALL
- http://dev.wifidog.org/wiki/doc/install/debian


## FreeRadius

    apt-get install freeradius


- http://freeradius.org/


## 3G Modem

### Debian Jessie x86

    xe1gyq@jessie:~$ lsusb
    Bus 001 Device 002: ID 046d:c31c Logitech, Inc. Keyboard K120 for Business
    Bus 002 Device 002: ID 046d:c05a Logitech, Inc. M90/M100 Optical Mouse
    Bus 006 Device 003: ID 148f:5370 Ralink Technology, Corp. RT5370 Wireless Adapter
    Bus 007 Device 003: ID 1bbb:011e T & A Mobile Phones 

    [  422.300054] usb 7-3: new high-speed USB device number 2 using ehci-pci
    [  422.434543] usb 7-3: New USB device found, idVendor=1bbb, idProduct=f017
    [  422.434547] usb 7-3: New USB device strings: Mfr=3, Product=2, SerialNumber=0
    [  422.434550] usb 7-3: Product: Mobile Broad Band
    [  422.434552] usb 7-3: Manufacturer: USBModem
    [  422.786231] usb-storage 7-3:1.0: USB Mass Storage device detected
    [  422.786448] scsi6 : usb-storage 7-3:1.0
    [  422.786541] usb-storage 7-3:1.1: USB Mass Storage device detected
    [  422.786587] scsi7 : usb-storage 7-3:1.1
    [  422.786674] usbcore: registered new interface driver usb-storage
    [  423.221714] usb 7-3: USB disconnect, device number 2
    [  426.436043] usb 7-3: new high-speed USB device number 3 using ehci-pci
    [  426.570781] usb 7-3: New USB device found, idVendor=1bbb, idProduct=011e
    [  426.570785] usb 7-3: New USB device strings: Mfr=3, Product=2, SerialNumber=0
    [  426.570788] usb 7-3: Product: Mobile Broad Band
    [  426.570791] usb 7-3: Manufacturer: USBModem
    [  426.574356] usb-storage 7-3:1.2: USB Mass Storage device detected
    [  426.574424] scsi8 : usb-storage 7-3:1.2
    [  426.679993] usbcore: registered new interface driver usbserial
    [  426.680219] usbcore: registered new interface driver usbserial_generic
    [  426.680236] usbserial: USB Serial support registered for generic
    [  426.696159] usbcore: registered new interface driver option
    [  426.696178] usbserial: USB Serial support registered for GSM modem (1-port)
    [  426.696297] option 7-3:1.0: GSM modem (1-port) converter detected
    [  426.696397] usb 7-3: GSM modem (1-port) converter now attached to ttyUSB0
    [  426.696437] option 7-3:1.1: GSM modem (1-port) converter detected
    [  426.696512] usb 7-3: GSM modem (1-port) converter now attached to ttyUSB1
    [  426.696554] option 7-3:1.3: GSM modem (1-port) converter detected
    [  426.696635] usb 7-3: GSM modem (1-port) converter now attached to ttyUSB2
    [  426.714412] usbcore: registered new interface driver cdc_wdm
    [  426.767392] qmi_wwan 7-3:1.4: cdc-wdm0: USB WDM device
    [  426.767604] qmi_wwan 7-3:1.4 wwan0: register 'qmi_wwan' at usb-0000:00:1d.7-3, WWAN/QMI device, 9a:a4:5e:7f:54:07
    [  426.767630] usbcore: registered new interface driver qmi_wwan
    [  427.573530] scsi 8:0:0:0: Direct-Access     USBModem MMC Storage      2.31 PQ: 0 ANSI: 2
    [  427.574461] sd 8:0:0:0: Attached scsi generic sg1 type 0
    [  427.577271] sd 8:0:0:0: [sdb] Attached SCSI removable disk
    
    [ 7259.343698] usb 7-3: GSM modem (1-port) converter now attached to ttyUSB6
[ 7259.345290] qmi_wwan 7-3:1.4: cdc-wdm0: USB WDM device
[ 7259.345547] qmi_wwan 7-3:1.4 wwan0: register 'qmi_wwan' at usb-0000:00:1d.7-3, WWAN/QMI device, 9a:a4:5e:7f:54:07
[ 7260.341716] scsi 11:0:0:0: Direct-Access     USBModem MMC Storage      2.31 PQ: 0 ANSI: 2
[ 7260.342729] sd 11:0:0:0: Attached scsi generic sg1 type 0
[ 7260.346072] sd 11:0:0:0: [sdb] Attached SCSI removable disk
[ 7520.623662] wlan0: deauthenticating from f8:01:13:a8:2b:40 by local choice (Reason: 3=DEAUTH_LEAVING)
[ 7520.669720] cfg80211: Calling CRDA to update world regulatory domain
[ 7520.731811] cfg80211: World regulatory domain updated:
[ 7520.731815] cfg80211:  DFS Master region: unset
[ 7520.731817] cfg80211:   (start_freq - end_freq @ bandwidth), (max_antenna_gain, max_eirp), (dfs_cac_time)
[ 7520.731819] cfg80211:   (2402000 KHz - 2472000 KHz @ 40000 KHz), (N/A, 2000 mBm), (N/A)
[ 7520.731821] cfg80211:   (2457000 KHz - 2482000 KHz @ 40000 KHz), (N/A, 2000 mBm), (N/A)
[ 7520.731823] cfg80211:   (2474000 KHz - 2494000 KHz @ 20000 KHz), (N/A, 2000 mBm), (N/A)
[ 7520.731825] cfg80211:   (5170000 KHz - 5250000 KHz @ 80000 KHz, 160000 KHz AUTO), (N/A, 2000 mBm), (N/A)
[ 7520.731828] cfg80211:   (5250000 KHz - 5330000 KHz @ 80000 KHz, 160000 KHz AUTO), (N/A, 2000 mBm), (0 s)
[ 7520.731829] cfg80211:   (5490000 KHz - 5730000 KHz @ 160000 KHz), (N/A, 2000 mBm), (0 s)
[ 7520.731831] cfg80211:   (5735000 KHz - 5835000 KHz @ 80000 KHz), (N/A, 2000 mBm), (N/A)
[ 7520.731833] cfg80211:   (57240000 KHz - 63720000 KHz @ 2160000 KHz), (N/A, 0 mBm), (N/A)

    
    lsusb
    Bus 007 Device 006: ID 1bbb:011e T & A Mobile Phones 
    
    usb-devices
    T:  Bus=07 Lev=01 Prnt=01 Port=02 Cnt=01 Dev#=  6 Spd=480 MxCh= 0
    D:  Ver= 2.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS=64 #Cfgs=  1
    P:  Vendor=1bbb ProdID=011e Rev=00.00
    S:  Manufacturer=USBModem
    S:  Product=Mobile Broad Band
    C:  #Ifs= 5 Cfg#= 1 Atr=e0 MxPwr=500mA
    I:  If#= 0 Alt= 0 #EPs= 2 Cls=ff(vend.) Sub=ff Prot=ff Driver=option
    I:  If#= 1 Alt= 0 #EPs= 2 Cls=ff(vend.) Sub=ff Prot=ff Driver=option
    I:  If#= 2 Alt= 0 #EPs= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage
    I:  If#= 3 Alt= 0 #EPs= 3 Cls=ff(vend.) Sub=ff Prot=ff Driver=option
    I:  If#= 4 Alt= 0 #EPs= 3 Cls=ff(vend.) Sub=ff Prot=ff Driver=qmi_wwan


### Debian Whezzy Intel Edison

    [  200.177110] usb 1-1.2: new high-speed USB device number 4 using dwc3-host
    [  200.203207] usb 1-1.2: New USB device found, idVendor=1bbb, idProduct=f017
    [  200.203240] usb 1-1.2: New USB device strings: Mfr=3, Product=2, SerialNumber=0
    [  200.203261] usb 1-1.2: Product: Mobile Broad Band
    [  200.203279] usb 1-1.2: Manufacturer: USBModem
    [  200.207677] usb-storage 1-1.2:1.0: USB Mass Storage device detected
    [  200.208398] scsi0 : usb-storage 1-1.2:1.0
    [  200.209556] usb-storage 1-1.2:1.1: USB Mass Storage device detected
    [  200.209970] scsi1 : usb-storage 1-1.2:1.1
    [  201.208324] scsi 1:0:0:0: CD-ROM            USBModem MMC Storage      2.31 PQ: 0 ANSI: 2
    [  201.210949] sr0: scsi-1 drive
    [  201.210973] cdrom: Uniform CD-ROM driver Revision: 3.20
    [  201.212360] sr 1:0:0:0: Attached scsi CD-ROM sr0
    [  201.213405] sr 1:0:0:0: Attached scsi generic sg0 type 5
    
    apt-get install ppp
    wget "http://www.sakis3g.com/downloads/sakis3g.tar.gz" -O sakis3g.tar.gz
    tar -xzvf sakis3g.tar.gz
    chmod +x sakis3g
    ./sakis3g --interactive
    
    root@ubilinux:~# modprobe usbserial vendor=0x1bbb product=0x0017
    root@ubilinux:~# lsmod
    Module                  Size  Used by
    ftdi_sio               40121  0 
    uvcvideo               71516  0 
    videobuf2_vmalloc      13003  1 uvcvideo
    videobuf2_memops       13001  1 videobuf2_vmalloc
    videobuf2_core         37707  1 uvcvideo
    usb_f_acm              14335  1 
    u_serial               18582  6 usb_f_acm
    g_multi                70813  0 
    libcomposite           39245  2 usb_f_acm,g_multi
    bcm_bt_lpm             13676  0 
    bcm4334x              578947  0 
    gedit /etc/udev/rules.d/50-myrules.rules
    ATTRS{idVendor}=="1bbb",ATTRS{idProduct}=="0017", RUN+="/sbin/modprobe usbserial vendor=0x1bbb product=0x0017"
    
    cat /sys/kernel/debug/usb/devices | more
    T:  Bus=01 Lev=02 Prnt=02 Port=01 Cnt=01 Dev#=  3 Spd=480  MxCh= 0
    D:  Ver= 2.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS=64 #Cfgs=  1
    P:  Vendor=1bbb ProdID=f017 Rev= 0.00
    S:  Manufacturer=USBModem
    S:  Product=Mobile Broad Band
    C:* #Ifs= 2 Cfg#= 1 Atr=c0 MxPwr=500mA
    I:* If#= 0 Alt= 0 #EPs= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=(none)
    E:  Ad=01(O) Atr=02(Bulk) MxPS= 512 Ivl=0ms
    E:  Ad=81(I) Atr=02(Bulk) MxPS= 512 Ivl=0ms
    I:* If#= 1 Alt= 0 #EPs= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage
    E:  Ad=02(O) Atr=02(Bulk) MxPS= 512 Ivl=0ms
    E:  Ad=82(I) Atr=02(Bulk) MxPS= 512 Ivl=0ms

    
    http://www.draisberghof.de/usb_modeswitch/
    
    nano /lib/udev/rules.d/40-usb_modeswitch.rules
    # Alcatel
    ATTRS{idVendor}=="1bbb", ATTRS{idProduct}=="011e", RUN+="usb_modeswitch '%b/%k'"






- http://www.sakis3g.com/
- https://wiki.archlinux.org/index.php/USB_3G_Modem
- http://www.draisberghof.de/usb_modeswitch/bb/viewtopic.php?f=4&t=1935
- http://www.draisberghof.de/usb_modeswitch/bb/viewtopic.php?t=952
- https://lawrencematthew.wordpress.com/2013/08/07/connect-raspberry-pi-to-a-3g-network-automatically-during-its-boot/

## Issues

    root@ubilinux:~/wifidog-auth# apt-get install postgresql-8.1
    E: Package 'postgresql-8.1' has no installation candidate


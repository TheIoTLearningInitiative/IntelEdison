WiFi
==

## Features

- Wi-Fi peer-to-peer connectivity with Wi-Fi Direct, Allows two Intel® Edison devices (or one Intel® Edison device and a smartphone) to create a direct Wi-Fi connection to each other without an access point.
- Wi-Fi multirole, Allows a connection to an access point simultaneously with Wi-Fi Direct operation. 
- Wi-Fi IBSS mode, Allows creation of multinode ad hoc networks that contain no access point.

## Kernel Display Message

    root@edison:~# dmesg | grep -i wifi
    [    0.189658] Using generic wifi platform data
    [    0.189675] wifi_platform_data: GPIO == 64
    [    3.850154] found wifi platform device wlan
    [    4.171606] wifi_platform_set_power = 1
    [    4.373687] wifi_platform_bus_enumerate device present 1
    [    4.412928] wifi_platform_get_mac_addr
    [    4.413069] wifi_get_mac_addr_intel: unable to open /config/wifi/mac.txt
    [    4.420354] wifi_platform_set_power = 0
    [    4.421428] wifi_platform_bus_enumerate device present 0
    [   38.194385] wl_android_wifi_on in
    [   38.194403] wifi_platform_set_power = 1
    [   39.117444] wifi_platform_get_mac_addr
    [   39.117488] wifi_get_mac_addr_intel: unable to open /config/wifi/mac.txt
    root@edison:~# lsmod
    Module                  Size  Used by
    usb_f_acm              14335  1 
    ...
    bcm_bt_lpm             13708  0 
    bcm4334x              587105  0 

## Userspace Applications
## Setup

Make sure there are no soft blocks

    root@edison:~# rfkill list

Make sure wlan0 is loaded and see IP

    root@edison:~# ifconfig

Load the wlan0 device driver

    root@edison:~# wpa_supplicant -B -Dnl80211 -iwlan0 -c/etc/wpa_supplicant/wpa_supplicant.conf

Get DHCP and DNS

    root@edison:~# busybox udhcpc -i wlan0

Move usb0 to a different non-conflicting subnet

    root@edison:~# vi /etc/system/system/basic.target.wants/network-gadget-init.service

Disable usb0 device from loading

    root@edison:~# systemctl disable network-gadget-init.service

Ensure there is a wpa_supplicant network{} definition and remove unneeded networks

    root@edison:~# vi /etc/wpa_supplicant/wpa_supplicant.conf
    
Enable first network definition

    root@edison:~# wpa_cli
         > enable_network 0
         > select_network 0
         > save
         > quit

Example WEP key wpa_supplicant.conf

    ctrl_interface=/var/run/wpa_supplicant
    ctrl_interface_group=0
    update_config=1
    network={
         ssid="YOURSSID"
         scan_ssid=1
         key_mgmt=NONE
         auth_alg=OPEN
         wep_key0=f0039faded348299992344be23
    }

Remove soft block on wlan0

    root@edison:~# rfkill unblock wlan

Enable wifi on boot once config is confirmed correct

    root@edison:~# systemctl enable wa_supplicant

WiFi to connect at power up:

    systemctl enable wpa_supplicant
    systemctl start wpa_supplicant

### Apt-Get
### Opkg
## Device Configuration
## Usage Models
## Links

- [Intel® Edison Boards Wi-Fi User Guide](http://www.intel.com/support/edison/sb/CS-035380.htm)
- https://software.intel.com/en-us/connecting-to-a-network-intel-edison-board

## Yocto Default Image

    root@Edison:~# configure_edison --wifi
     Configure Edison: WiFi Connection
    root@edison:~# ifconfig
     lo        Link encap:Local Loopback
               inet addr:127.0.0.1  Mask:255.0.0.0
     ...
     usb0      Link encap:Ethernet  HWaddr 5a:2a:15:c5:5f:7b
               inet addr:192.168.2.15  Bcast:192.168.2.255  Mask:255.255.255.0
     ...
     wlan0     Link encap:Ethernet  HWaddr 78:4b:87:a6:cf:5e
               inet addr:192.168.1.68  Bcast:0.0.0.0  Mask:255.255.255.0
    root@edison:~# ping google.com



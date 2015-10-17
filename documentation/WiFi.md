WiFi
==

- Wi-Fi peer-to-peer connectivity with Wi-Fi Direct, Allows two Intel® Edison devices (or one Intel® Edison device and a smartphone) to create a direct Wi-Fi connection to each other without an access point.
- Wi-Fi multirole, Allows a connection to an access point simultaneously with Wi-Fi Direct operation. 
- Wi-Fi IBSS mode, Allows creation of multinode ad hoc networks that contain no access point.

## Kernel Integration
## Userspace Applications
## Setup

Make sure there are no soft blocks
    ~# rfkill list
Make sure wlan0 is loaded and see IP
    ~# ifconfig
Load the wlan0 device driver
    ~# wpa_supplicant -B -Dnl80211 -iwlan0 -c/etc/wpa_supplicant/wpa_supplicant.conf
Get DHCP and DNS
    ~# busybox udhcpc -i wlan0
Move usb0 to a different non-conflicting subnet
    ~# vi /etc/system/system/basic.target.wants/network-gadget-init.service
Disable usb0 device from loading
    ~# systemctl disable network-gadget-init.service
Ensure there is a wpa_supplicant network{} definition and remove unneeded networks
    ~# vi /etc/wpa_supplicant/wpa_supplicant.conf
Enable first network definition
    ~# wpa_cli
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
    ~# rfkill unblock wlan
Enable wifi on boot once config is confirmed correct
    ~# systemctl enable wa_supplicant

WiFi to connect at power up:

    systemctl enable wpa_supplicant
    systemctl start wpa_supplicant

### Apt-Get
### Opkg
## Device Configuration
## Usage Models
## Links

- https://software.intel.com/en-us/connecting-to-a-network-intel-edison-board
- http://download.intel.com/support/edison/sb/edison_wifi_331438001.pdf
- http://www.intel.com/support/edison/sb/CS-035380.htm

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



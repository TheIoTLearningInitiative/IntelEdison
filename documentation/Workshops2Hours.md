# 2 Hours

# Flashing

Requirements

- [Installers](https://software.intel.com/en-us/iot/hardware/edison/downloads)
  - Double click
    - Select "USB drivers installed"
    - Finish
  - Firmware version installed: not detected. Latest available: 201606061707
    - Flash Firmware
      - C:\Intel\Edison\Image\edison-image-20160606
      - Use existing image located at 

# Booting

```sh
Poky (Yocto Project Reference Distro) 1.7.3 edison ttyMFD2                      
                                                                                
edison login: root                                                              
Last login: Mon Jun  6 21:33:16 UTC 2016 on ttyMFD2
```

Check your kernel version

```sh
root@edison:~# uname -r                                                         
3.10.98-poky-edison+                                                            
root@edison:~# 

```

Configure your Edison WiFi network

```sh
root@edison:~# configure_edison --wifi
Configure Edison: WiFi Connection

Scanning: 1 seconds left  

0 :     Rescan for networks
1 :     Exit WiFi Setup
2 :     Manually input a hidden SSID
3 :     CACUNAT
4 :     INFINITUMf89t
5 :     INFINITUM09E845
6 :     17057Abril
7 :     INFINITUMndjj
8 :     INFINITUMfjph


Enter 0 to rescan for networks.
Enter 1 to exit.
Enter 2 to input a hidden network SSID.
Enter a number between 3 to 8 to choose one of the listed network SSIDs: 8
Is INFINITUMfjph correct? [Y or N]: Y
Password must be between 8 and 63 characters.
What is the network password?: **********
Initiating connection to INFINITUMfjph. Please wait...                          
Attempting to enable network access, please check 'wpa_cli status' after a minu.
Done. Please connect your laptop or PC to the same network as this device and g.
Warning: SSH is not yet enabled on the wireless interface. To enable SSH access.
root@edison:~# 
```

```sh
root@edison:~# ping -c 2 8.8.8.8                                                
PING 8.8.8.8 (8.8.8.8): 56 data bytes                                           
64 bytes from 8.8.8.8: seq=0 ttl=59 time=151.659 ms                             
64 bytes from 8.8.8.8: seq=1 ttl=59 time=43.713 ms                              
                                                                                
--- 8.8.8.8 ping statistics ---                                                 
2 packets transmitted, 2 packets received, 0% packet loss                       
round-trip min/avg/max = 43.713/97.686/151.659 ms                               
root@edison:~# 
```

# Project Cloning

https://github.com/xe1gyq/TheIoTLearningInitiative.git


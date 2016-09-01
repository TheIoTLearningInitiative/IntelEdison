# We Are Bimbo

# Requirements

- Who We Are!
  - Name your team
  - Choose a slogan
- Hardware
  - Laptop
  - Internet Connection
  - Intel Edison 
  - [Grove Indoor Environment Kit for Intel® Edison](https://www.seeedstudio.com/item_detail.html?p_id=2427)
- Team Specialists
  - Hardware
  - Embedded Software
  - Cloud
  - Marketing
  - Presenter
- Challenge
  - Integrate all components
  - First team to deliver data to our Somos Bimbo Dashboard Wins!

# Hardware Specialist

- Laptop
- Internet Connection
- Intel Edison
- [Grove Indoor Environment Kit for Intel® Edison](https://www.seeedstudio.com/item_detail.html?p_id=2427)
  - [Grove - Light Sensor](http://www.seeedstudio.com/wiki/Grove_-_Light_Sensor)
    v![](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/cover.jpg)
  - [Grove - LCD RGB Backlight](http://www.seeedstudio.com/wiki/Grove_-_LCD_RGB_Backlight)
    ![](https://raw.githubusercontent.com/SeeedDocument/Grove_LCD_RGB_Backlight/master/images/intro.jpg)

# Embedded Software Specialist


```sh
...
[  OK  ] Reached target Multi-User System.
         Starting Redis Server...
[  OK  ] Started Redis Server.

Poky (Yocto Project Reference Distro) 1.7.3 edison ttyMFD2

edison login: 
```

Enter your username as root, no password is required

```sh
edison login: root
root@edison:~# 
```

Shutdown usb0 interface

```
root@edison:~# ifconfig usb0 down
```

Configure your WiFi

```sh
root@edison:~# configure_edison --wifi
```

```sh
Configure Edison: WiFi Connection

Scanning: 1 seconds left

0 :     Rescan for networks
1 :     Exit WiFi Setup
2 :     Manually input a hidden SSID
3 :     Guest
4 :     TP-LINK_2A2C7A
5 :     LabWLAN
6 :     EmployeeHotspot
7 :     TSNOfficeWLAN
8 :     RSN2OfficeWLAN
9 :     IOT-Lab


Enter 0 to rescan for networks.
Enter 1 to exit.
Enter 2 to input a hidden network SSID.
Enter a number between 3 to 9 to choose one of the listed network SSIDs: 6
Is EmployeeHotspot correct? [Y or N]: Y
Please enter the network username: hs_11342026_2
What is the network password?: ********
Initiating connection to EmployeeHotspot. Please wait...

...


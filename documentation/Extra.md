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

- http://www.sakis3g.com/
- https://wiki.archlinux.org/index.php/USB_3G_Modem
- http://www.draisberghof.de/usb_modeswitch/bb/viewtopic.php?f=4&t=1935
- http://www.draisberghof.de/usb_modeswitch/bb/viewtopic.php?t=952

## Issues

    root@ubilinux:~/wifidog-auth# apt-get install postgresql-8.1
    E: Package 'postgresql-8.1' has no installation candidate


Extra
==

Setup

- Configure Wireless LAN


    apt-get update
    apt-get install git
    apt-get usb-modeswitch
    apt-get install build-essential g++ automake autoconf gnu-standards autoconf-doc libtool gettext autoconf-archive
    apt-get install wvdial

## Squid Proxy

> Squid is a caching proxy for the Web supporting HTTP, HTTPS, FTP, and more. It reduces bandwidth and improves response times by caching and reusing frequently-requested web pages. Squid has extensive access controls and makes a great server accelerator. It runs on most available operating systems, including Windows and is licensed under the GNU GPL.


    apt-get install squid3 squid3-common


- http://linuxaria.com/pills/how-to-setup-a-squid-proxy-on-your-debian-linux

## DHCP


    apt-get install dhcpd


## Apache


    apt-get install apache2


## WifiDog

    git clone https://github.com/wifidog/wifidog-gateway.git
    ./autogen.sh
    ./configure
    make
    make install
    


https://github.com/wifidog/wifidog-auth/blob/master/INSTALL
http://dev.wifidog.org/wiki/doc/install/debian


## FreeRadius

    apt-get install freeradius


Open Package Management
==

    root@edison:~# vi /etc/opkg/base-feeds.conf
    src/gz all http://repo.opkg.net/edison/repo/all
    src/gz edison http://repo.opkg.net/edison/repo/edison
    src/gz core2-32 http://repo.opkg.net/edison/repo/core2-32
    root@edison:~# opkg update
     Downloading http://iotdk.intel.com/repos/1.1/iotdk/all/Packages.
     Updated list of available packages in /var/lib/opkg/all.
     Downloading http://iotdk.intel.com/repos/1.1/iotdk/x86/Packages.
     Updated list of available packages in /var/lib/opkg/x86.
     Downloading http://iotdk.intel.com/repos/1.1/iotdk/i586/Packages.
     Updated list of available packages in /var/lib/opkg/i586.
    root@edison:~# opkg install nano
    root@edison:~# opkg install git
    root@edison:~# opkg list-installed | grep mraa
    root@edison:~# opkg list-installed | grep upm
    root@edison:~# git config --global user.name "Name LastName"
    root@edison:~# git config --global user.email email@adress.com
    root@edison:~# opkg install libsdl-1.2-dev libv4l-dev
    root@edison:~# opkg install fswebcam

root@edison:~# opkg install cmake espeak nano

    root@edison:~# wget http://repo.opkg.net/edison/repo/core2-32/less_458-r0_core2-32.ipk
    root@edison:~# opkg install bash_4.3-r0_core2-32.ipk

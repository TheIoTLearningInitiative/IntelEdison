BootUp
==

    abraham@aarcemor-desk:~$ sudo minicom -D /dev/ttyUSB0 115200
    

## Bootup Message

******************************
PSH KERNEL VERSION: b0182b2b
                WR: 20104000
******************************

SCU IPC: 0x800000d0  0xfffce92c

PSH miaHOB version: TNG.B0.VVBD.0000000c

microkernel built 11:24:08 Feb  5 2015

******* PSH loader *******CM page cache size = 192 KB 
Cache Constrais
Arming IPC driver ..
Adding page store pool ..
PagestoreAddr(IMR Start Address) = 0x04899000
pagIMR Size)          = 0dy to receive application *** 


U-Boot 2014.04 (Dec 19 2015 - 23:30:32)

       Watchdog enabled
DRAM:  980.6 MiB
MMC:   tangier_sdhci: 0
In:    serial
Out:   serial
Err:   serial
Hit any key to stop autoboot:  0 
Target:blank
Partitioning already done...
Flashing already done...
GADGET DRIVER: usb_dnl_dfu
reading vmlinuz
5385504 bytes read in 133 ms (38.6 MiB/s)
Valid Boot Flag
Setup Size = 0x00003c00
Magic signature found
Using boot protocol version 2.0c
Linux kernel version 3.10.17-yocto-standard (abraham@aarcemor-desk) #1 SMP PREEMPT Sat Dec 19 23:23:25 CST 2015
Building boot_params at 0x00090000
Loading bzImage at address 00100000 (5370144 bytes)
Magic signature found
Kernel command line: "rootwait root=PARTUUID=012b3303-34ac-284d-99b4-34e03a2335f4 rootfstype=ext4 console=ttyMFD2 earlyprintk=ttyMFD2,k"

Starting kernel ...

[    0.766587] pca953x 1-0020: failed reading register
[    0.771661] pca953x 1-0021: failed reading register
[-0022: failed reading register
[    0.781845] pca953x 1-0023: failed reading register
[    1.621706] snd_soc_sst_platform: Enter:sst_soc_probe
[    2.026053] pmic_ccsm pmic_ccsm: Error reading battery profile from battid frmwrk
[    2.044225] pmic_ccsm pmic_ccsm: Battery Over heat exception

Welcome to Linux!

         Expecting device dev-ttyMFD2.device...
[  OK  ] Reached target Remote File Systems.
         Expecting device dev-disk-by\x2dpartlabel-factory.device...
         Expecting device sys-subsystem-net-devices-usb0.device...
[  OK  ] Reached target Paths.
[  OK  ] Reached target Swap.
[  OK  ] Set up automount boot.automount.
[  OK  ] Created slice Root Slice.
[  OK  ] Created slice User and Session Slice.
[  OK  ] Listening on Delayed Shutdown Socket.
[  OK  ] Listening on /dev/initctl Compatibility Named Pipe.
[  OK  ] Listening on udev Kernel Socket.
[] Listeninontrol Socke[] Listeninl Socket.
[m] Createdm Slice.
       Mountry Director[  OKted slice s\x2dgetty.s[  OK ed slice system-getty.slice.
arting Appliables...
         Starting Load Kernel Modules...
      System...
         Mounting POSIX Message ystem...
         Starting udev Coldplug all Devices...
     g Create lised static de.rrent kern         Starting Journal Service...
  OK  ]rnal Service.
      Remount Roo File Systems...
2m  OK  tomount home.automount.[] Mounted POSIX Message System.
m  OK  ] Mounted Debug File System.
[  OK  ] Mounted Temporary Directory.
[m] Started Apply Kerne.
[  OK   required static device nodes ...current kernel.
[  OK  ] Sta Root and Kernel File Systems.
[  OK  ] Started Load Kernel Modules.
[  OK  ] Started udev Coldplug all Devices.
         Mounting Configuration File System...
         Mounting FUSE Control File System..     Starting Load/Save Random Seed...
         Device Nodes in /dev...
[  unted FUSE Control File System.
[  OK  ] Mounted Configuration File System.
[ /Save Random Seed.
[  OK  ] ate Static Device Nodes in /dev.
         Starting udev Kernel Device Manager...
[  OK  ] Reached target Local         Mounting /var/volatile...
K  ] Started udev Kernel Device Manager.
[  OK  ] Reached target Local File Systems.
         Starting Create Volatile Files and Directories...
         Starting Trigger Flushing of Journal to Persistent Storage...
[  OK  ] Started Create Volatile Files and Directories.
[  OK  ] Started Trigger Flushing of Journal to Persistent Storage.
[  OK  ] Found device /sys/subsystem/net/devices/usb0.
[  OK  ] Found device /dev/ttyMFD2.
[  OK  ] Created slice system-systemd\x2drfkill.slice.
         Starting Load/Save RF Kkill2...
         Starting Load/Save RF Kill Switch Status of rfkill1...
        ad/Save RF Status of r      Network Tization...
         Star UTMP about System Boot/Shutdown...
[  OK  ] Started Load/Save RF Kill Switch Status of rfkill2.
[  OK  ] Started Load/Save RF Kill Switch Status of rfkill1.
[  OK  ] Started Load/Save RF Kill Switch Status of rfkill0.
[  OK  ] Started Network Time Synchronization.
[  OK  ] Found device /dev/disk/by-partlabel/factory.
[  OK  ] Started Update UTMP about System Boot/Shutdown.
[  OK  ] Reached target Sound Card.
         Mounting Mount for factory...
[  O
[  OK  ]on RPCbind Server Activation Socket.
[  OK  ] Listening on D-Bus System Message Bus Socke[  OK  ] Reached target Timers.
         Starting Restore Sound Card State...
[  OK  ] Mounted Mount for factory.
[  OK  ] Listening on sshd.socket.
[  OK  ] Created slice system-systemd\x2dfsck.slice.
         StSystem Checsk/by-partlabel/home...[ eached targ
                                                          K  ] Rea Basic System.
       Starting Edison PWR button [  OK  ed Edison PWndler.
rting Telephony service   Starting Daemon to handle arduinarduino sketches.
         Starting Start orP Mode in Edison...
[pp binary.tarting Dae sketches..K  ] St to reset sketches.
         Starervice...
         Starting D-Bus System Message Bus...
[  OK  ] Started D-Bus System Message Bus.
Application available at (physical) a819000
        VRL mapped to 0xff217000
        App size = 11508 App Authentture is dis Resetting IPC

** receive ap** 
484] syste
[    stem
[  OK  ] Started Telee.
     Starting Network   ing Cleanjoe...
[  OK  ed Cleanjournal service.
         Starting Crashlog [[0m] Started Crashlog service.
         S[  OK  ] Started Watchdog sample daemon.
         Starting Permit User Ses[  OK  ] Started Network Service.
[  OK  ] Started File System Check on /dev/disk/by-partlabel/home.
[  OK  ] Started Permit User Sessions.
[  OK  ] Started Login Service.
 Bluetooth service...
         Starting File System Check on /dev/disk/by-partlabel/boot...
         Starting Serial Getty on ttyMFD2...
[  OK  ] Started Serial Getty on ttyMFD2.
         Starting Getty on tty1...
[  OK  ] Started Getty on tty1.
[  OK  ] Reached target Login Prompts.
         Mounting /home...
         Starting Network Name Resolution...
[  OK  ] Reached target Network.
         Starting Zero-configuration networking...
         Starting Mosquitto - lightweight server implementati...SN protocols...
[    9.569433] systemd-fsck[225]: dosfsck 2.11, 12 Mar 2005, FAT32, LFN
[    9.576079] systemd-fsck[225]: /dev/mmcblk0p7: 5 files, 2718/2947 clusters
[  OK  [32m  OK  File System Check on /dev/disk/by-partlabel/boot.
[  OK  ] Mounted /home.
[  OK  ] Started Mosquitto - lightweight server implementatio...T-SN protocols.
[  OK  ] Started Zero-configuration networking.
[  OK  ] Started Bluetooth service.
[  OK  ] Started Restore Sound Card State.
         Starting PulseAudio Sound System...
 Starting Horting The Edison status and configuration service...
[  OK  ] Started The Edison onfiguration service.
         Starting Intel_XDK_Daemon...
[  OK  ] Started Intel_XDK_Daemon.
         Mounting /boot...
[  OK  ] Started Hostname Service.
[  OK  ] Mounted /boot.
[  OK  ] Started PulseAudio Sound System.
[[0m] Reached target Multi-User System.

Poky (Yocto Project Reference Distro) 1.7.2 edison ttyMFD2

edison login: 


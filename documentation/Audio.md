Sound
==

## Kernel Integration
## Userspace Applications

    root@edison:~# lsusb

## Setup
### Opkg

    root@edison:~# opkg install alsa-utils
    root@edison:~# ls /usr/share/sounds/alsa/

### Apt-Get

    root@edison:~# apt-get install alsa-utils

## Device Configuration

    root@edison:~# vi ~/.asoundrc
    root@edison:~# vi /etc/asound.conf
    pcm.!default sysdefault:Headset
    ~/.asoundrc file.
    pcm.!default {
        type plug
        slave {
            pcm “hw:2,0”
        }
    }

## Usage Models

    root@edison:~# aplay -Ll
    root@edison:~# aplay /usr/share/sounds/alsa/Front_Center.wav
    root@edison:~# aplay -D hw:1,0 /usr/share/sounds/alsa/Front_Center.wav
    root@edison:~# mpg123

## Links

- http://repo.opkg.net/edison/repo/edison/kernel-module-snd-usb-audio_3.10.17+git0+6ad20f049a_c03195ed6e-r0_edison.ipk


## Tbd

    sudo modprobe -v snd_usb_audio
    sudo modprobe --force-vermagic snd-usb-audio.ko
    sudo depmod -a
    sudo alsactl init
    sudo alsa-utils stop/start
    sudo dpkg-reconfigure alsa-base
    cat /dev/sndstat
    cat /proc/asound/cards
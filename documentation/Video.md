Camera
==

## Kernel Integration

    root@edison:~# lsmod
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
    root@edison:~# find /lib/modules/* -name 'uvc'
    

## Userspace Applications

    root@edison:~# ffmpeg

## Setup

    root@edison:~# find /lib/modules/* -name 'uvc'

### Opkg

    root@edison:~# opkg install kernel-module-uvcvideo
    root@edison:~# lsmod | grep uvc

### Apt-Get

## Device Configuration

    root@edison:~# lsmod | grep uvc
    root@edison:~# ls -al /dev/video0

## Usage Models

### IP Webcam

## Links

- https://www.ffmpeg.org/

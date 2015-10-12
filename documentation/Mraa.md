MRAA
==

## Yocto Setup

    root@Edison:~# git clone https://github.com/intel-iot-devkit/mraa.git
    root@edison:~# mkdir mraa/build && cd $_
    root@edison:~# cmake ..
    root@edison:~# make
    root@edison:~# make install
    root@edison:~# nano /etc/ld.so.conf
    /usr/local/lib/i386-linux-gnu/
    root@edison:~# ldconfig
    root@edison:~# ldconfig -p | grep mraa
    root@edison:~# export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))
    root@edison:~# nano ~/.bashrc
    export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))

## Ubilinux Setup

    root@Edison:~# apt-get update
    root@Edison:~# apt-cache search pcre
    root@Edison:~# apt-get install libpcre3-dev
    root@Edison:~# apt-get install git
    root@Edison:~# apt-get install cmake
    root@Edison:~# apt-get install python-dev
    root@Edison:~# apt-get install swig
    root@Edison:~# git clone https://github.com/intel-iot-devkit/mraa.git
    root@Edison:~# mkdir mraa/build && cd $_
    root@Edison:~# cmake .. -DBUILDSWIGNODE=OFF
    root@Edison:~# make
    root@Edison:~# make install
    root@Edison:~# cd
    root@edison:~# nano /etc/ld.so.conf
    /usr/local/lib/i386-linux-gnu/
    root@edison:~# ldconfig
    root@edison:~# ldconfig -p | grep mraa
    root@edison:~# export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))
    root@edison:~# nano ~/.bashrc
    export PYTHONPATH=$PYTHONPATH:$(dirname $(find /usr/local -name mraa.py))

Based on [Installing libmraa on Ubilinux for Edison](https://learn.sparkfun.com/tutorials/installing-libmraa-on-ubilinux-for-edison)
 
## Mraa Testing

    root@edison:~# cd mraa/examples
    root@edison:~# gcc -lmraa hellomraa.c -o hellomraa
    root@edison:~# ./hellomraa
     hello mraa
      Version: v0.6.2
      Running on Intel Edison

## Links

 - [MRAA Github](https://github.com/intel-iot-devkit/mraa)
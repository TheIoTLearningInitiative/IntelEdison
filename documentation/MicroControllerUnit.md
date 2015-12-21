Micro Controller Unit
==

## Microcontroller Unit SDK

    user@host:~$ ls edison-src/meta-intel-edison/meta-intel-edison-bsp/recipes-support/edison-mcu/
    files  mcu-fw-bin_0.1.bb  mcu-fw-load_0.1.bb
    user@host:~$ ls meta-intel-edison/meta-intel-edison-bsp/recipes-support/edison-mcu/files/
    intel_mcu.bin  mcu_fw_loader.service  mcu_fw_loader.sh
    user@host:~$ cat meta-intel-edison/meta-intel-edison-bsp/recipes-support/edison-mcu/files/mcu_fw_loader.service
    [Unit]
    Description=Daemon to load edison mcu app binary
    After=syslog.target
    
    [Service]
    ExecStart=/etc/intel_mcu/mcu_fw_loader.sh
    
    [Install]
    WantedBy=multi-user.target
    user@host:~$ cat meta-intel-edison/meta-intel-edison-bsp/recipes-support/edison-mcu/files/mcu_fw_loader.sh

```sh
#!/bin/sh
#author: JiuJin Hong (jiujinx.hong@intel.com)
if [ ! -d "/sys/devices/platform/intel_mcu" ];then
	exit
fi

if [ ! -f "/lib/firmware/intel_mcu.bin" ];then
	exit
fi

echo "load mcu app" > /sys/devices/platform/intel_mcu/control
```


    root@edison:~# ls /sys/devices/platform/intel_mcu/ 
    control     fw_version  modalias    subsystem   uevent
    driver      log_level   power       tty




     drivers/hwmon/intel_mcu_common.c                   |  700 +++
     drivers/hwmon/intel_mcu_common.h                   |   79 +
     drivers/hwmon/intel_mid_gpadc.c                    | 1212 ++++


### Feature Set

- **Onboard MCU** Viper RTOS Adds deterministic behavior to Linux* applications as a service. 
- **SDK access to UART, I2C, and all deviceGPIOs** Connects to a variety of sensors and extended interfaces
- **SDK Interprocessor Communication (IPC) messaging with CPU wake** Uses the MCU to filter sensor data, then wakes up the CPU for further analytics 

    /sys/devices/platform/intel_mcu

## Links

- [Creating applications with the MCU SDK for the Intel® Edison board](https://software.intel.com/en-us/creating-applications-with-mcu-sdk-for-intel-edison-board)
- https://software.intel.com/en-us/node/557537
- http://download.intel.com/support/edison/sb/edison_rn_332032008.pdf
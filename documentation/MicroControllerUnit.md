Micro Controller Unit
==

## Kernel Integration

    root@edison:~# ls /sys/devices/platform/intel_mcu/ 
    control     fw_version  modalias    subsystem   uevent
    driver      log_level   power       tty
    
    root@edison:~# dmesg | grep -i mcu
    [    1.001624] MCU detected and ready to used!


## Source Code

### Patch

#### Files

     drivers/hwmon/intel_mcu_common.c                   |  700 +++
     drivers/hwmon/intel_mcu_common.h                   |   79 +

#### .config

    +CONFIG_INTEL_MCU=y

#### Kconfig

    +config INTEL_MCU
    +       tristate "Intel generic MCU control interface"
    +       help
    +         Say Y here to enable control interface for intel mcu
    + 
    +         This driver provide userspace tty interface for the control and
    +         message output.
    +         You could use normal read/write to complete those operation.

#### Makefile

    +obj-$(CONFIG_INTEL_MCU)        += intel_mcu_common.o

### Driver

#### Name

    +       .driver = {
    +               .name   = "intel_mcu",
    +       },

#### Commands

    +enum cmd_id {
    +       CMD_MCU_LOAD_APP = 0,
    +       CMD_MCU_SETUP_DDR,
    +       CMD_MCU_APP_DEBUG,
    +       CMD_MCU_APP_GET_VERSION,
    +};


#### Command Handling

    +               case CMD_MCU_APP_GET_VERSION:
    +               case CMD_MCU_APP_DEBUG:

    root@edison:~# cat /sys/devices/platform/intel_mcu/fw_version 
    1.0.10

#### Debug Level

    +static char *debug_msg[] = {
    +       "fatal",
    +       "error",
    +       "warning",
    +       "info",
    +       "debug",
    +};

    root@edison:~# cat /sys/devices/platform/intel_mcu/log_level 
    info
    root@edison:~# echo debug > /sys/devices/platform/intel_mcu/log_level 
    root@edison:~# cat /sys/devices/platform/intel_mcu/log_level 
    debug

## Yocto Recipes

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

### Feature Set

- **Onboard MCU** Viper RTOS Adds deterministic behavior to Linux* applications as a service. 
- **SDK access to UART, I2C, and all deviceGPIOs** Connects to a variety of sensors and extended interfaces
- **SDK Interprocessor Communication (IPC) messaging with CPU wake** Uses the MCU to filter sensor data, then wakes up the CPU for further analytics 

    /sys/devices/platform/intel_mcu

## Links

- [Creating applications with the MCU SDK for the Intel® Edison board](https://software.intel.com/en-us/creating-applications-with-mcu-sdk-for-intel-edison-board)
- https://software.intel.com/en-us/node/557537
- http://download.intel.com/support/edison/sb/edison_rn_332032008.pdf
Microcontroller Unit
==

> Host CPU, On Intel® Edison, the Intel® Atom™ processor that runs on Linux OS

> Viper. An Intel (Wind River) real-time operating system that runs on the MCU. It provides basic OS function support, including thread scheduling, memory management, interrupt dispatch, and so on...

> MCU, Microcontroller unit. On the Intel® Edison board, this is a “Minute IA” 32-bit CPU

> MCU Application, Application that runs on an MCU. In most cases, it implements the expected features (controlling GPIOs, getting data from sensors, etc.)

> The scheduler in a Real Time Operating System (RTOS) is designed to provide a predictable (normally described as deterministic) execution pattern. This is particularly of interest to embedded systems as embedded systems often have real time requirements. A real time requirements is one that specifies that the embedded system must respond to a certain event within a strictly defined time (the deadline). A guarantee to meet real time requirements can only be made if the behaviour of the operating system's scheduler can be predicted (and is therefore deterministic).

## MCU SDK

The best MCU Reference Document to review is:

- [Creating applications with the MCU SDK for the Intel® Edison board](https://software.intel.com/en-us/creating-applications-with-mcu-sdk-for-intel-edison-board)

### Feature Set

- **Onboard MCU** Viper RTOS Adds deterministic behavior to Linux* applications as a service. 
- **SDK access to UART, I2C, and all GPIOs** Connects to a variety of sensors and extended interfaces
- **SDK Interprocessor Communication (IPC) messaging with CPU wake** Uses the MCU to filter sensor data, then wakes up the CPU for further analytics

## Kernel Integration

```sh
    root@edison:~# dmesg | grep -i mcu
    [    1.001624] MCU detected and ready to used!

    root@edison:~# ls /sys/devices/platform/intel_mcu/ 
    control     fw_version  modalias    subsystem   uevent
    driver      log_level   power       tty
```

### Firmware

```sh
    root@edison:~# configure_edison --help
    ...
      --version             Gets the current firmware version
      --latest-version      Gets the latest firmware version
    ...
    root@edison:~# configure_edison --version
    Could not determine firmware version information. Quitting.
    none

    root@edison:~# configure_edison --latest-version
    Could not determine firmware version information.
    Could not retrieve latest firmware version information. Quitting.
    none
```

### Tools

```sh
    root@edison:~# ls /etc/intel_mcu/mcu_fw_loader.sh
    root@edison:~# file /lib/firmware/intel_mcu.bin
```

### Interrupt Service Routine

```sh
    root@edison:~# cat /proc/interrupts | grep intel_psh_ipc
    47:         17          0   IO-APIC-fasteoi   intel_psh_ipc
```

### SysFs Power Interfaces

    root@edison:~# echo auto > /sys/devices/pci0000\:00/0000\:00\:04.3/power/control
    root@edison:~# echo on > /sys/devices/pci0000\:00/0000\:00\:04.3/power/control

## Userspace Communications

- __/dev/ttymcu0__ Channel for communication. Because of the exchange program on the microcontroller is carried out by means of functions and host_send host_receive.
- __/dev/ttymcu1__ Channel through which the microcontroller sends debugging messages function debug_print.
- __/dev/ttymcu2__ ...


    root@edison:~# cat /dev/ttymcu1
    (279940000,DEBUG): CUST IPC:12(c0000000, 72617473)
    (279941000,DEBUG): ipc process succeed
    (279960000,DEBUG): CUST IPC:12(80000000, 72610a74)
    (279961000,DEBUG): ipc process succeed


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

Explore the internal tools from Eclipse to work with Edison MCU

- [Edison MCU Internal Tools](https://github.com/lambdasakura/irremocon-edison/tree/master/internal_tools)


## Links

- [Creating applications with the MCU SDK for the Intel® Edison board](https://software.intel.com/en-us/creating-applications-with-mcu-sdk-for-intel-edison-board)
- https://software.intel.com/en-us/node/557537
- http://download.intel.com/support/edison/sb/edison_rn_332032008.pdf
- http://habranews.net/inteledison.html
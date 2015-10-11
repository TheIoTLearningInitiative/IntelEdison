Power
==

## Kernel Integration

    root@edison:~# ls /sys/power/
    pm_async           pm_print_times     state              wake_unlock
    pm_freeze_timeout  pm_test            wake_lock          wakeup_count

## Userspace Applications

    root@edison:~# systemctl poweroff
    root@edison:~# cat /sys/module/pcie_aspm/parameters/policy
    default [performance] powersave 

## Setup
### Apt-Get
### Opkg
## Device Configuration
## Usage Models
## Links

- [ACPI Wikipedia](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface)
- http://www.helios.de/heliosapp/edison/index.html
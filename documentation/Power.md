Power
==

> The Intel® Edison board has a known error on all UARTs. When Edison goes into low power sleep, the UART internal FIFO and interface is powered down. Therefore, a two-wire UART (Rx/Tx) will lose the first received character whenever Edison is in sleep mode. In order to avoid this condition, when sleep mode is enabled, a four-wire UART (Rx, Tx, CTS, and RTS) is required.


## Kernel Integration

    
    root@edison:~# rfkill block Bluetooth # BlueTooth
    
    root@edison:~# modprobe -r bcm4334x # WiFi
    root@edison:~# modprobe bcm4334x # WiFi
    
    root@edison:~# /sbin/iwconfig wlan0 power off
    root@edison:~# /sbin/iwconfig wlan0 power on 
    
    root@edison:~# cat /sys/power/state 
    freeze mem
    root@edison:~# cat /sys/power/pm_test
    [none] core processors platform devices freezer

    root@edison:~# echo 1 > /sys/devices/system/cpu/offline 

    root@edison:~# ls /sys/power/
    pm_async           pm_print_times     state              wake_unlock
    pm_freeze_timeout  pm_test            wake_lock          wakeup_count
    root@edison:~# cat /sys/devices/system/cpu/     
    cpu0/       cpuidle/    offline     power/      release     
    cpu1/       kernel_max  online      present     uevent      
    cpufreq/    modalias    possible    probe
    root@edison:~# ls /sys/devices/system/cpu/cpu0/cpufreq/                         
    affected_cpus                  scaling_cur_freq
    cpuinfo_cur_freq               scaling_driver
    cpuinfo_max_freq               scaling_governor
    cpuinfo_min_freq               scaling_max_freq
    cpuinfo_transition_latency     scaling_min_freq
    related_cpus                   scaling_setspeed
    scaling_available_frequencies  stats
    scaling_available_governors
    root@edison:~# cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors
    ondemand userspace performance
    root@edison:~# cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies
    500000
    
    
    root@edison:~# echo "mem" > /sys/power/state
    [23496.070128] pci_pm_suspend(): sdhci_pci_suspend+0x0/0xd0 returns -16
    [23496.070144] dpm_run_callback(): pci_pm_suspend+0x0/0x1d0 returns -16
    [23496.070158] PM: Device 0000:00:01.3 failed to suspend async: error -16
    [23496.091362] PM: Some devices failed to suspend
    -sh: echo: write error: Device or resource busy




## Userspace Applications

    root@edison:~# systemctl poweroff
    root@edison:~# cat /sys/module/pcie_aspm/parameters/policy
    default [performance] powersave 
    root@edison:~# cpufreq-info

## Setup
### Apt-Get
### Opkg
## Device Configuration
## Usage Models
## Links

- [ACPI Wikipedia](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface)
- http://www.helios.de/heliosapp/edison/index.html
- https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt
- https://www.kernel.org/doc/Documentation/power/states.txt
- https://www.kernel.org/doc/Documentation/power/basic-pm-debugging.txt
- https://communities.intel.com/thread/61067
- performance states (P-states) or power saving states (C-states)
- Dongle Host Driver, version 1.141.59 (r)
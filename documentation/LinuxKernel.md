Owner: Abraham

> Intel Silvermont (Atom)

> Mobile Internet Device(MID)

> Medfield is the follow-up of Moorestown, it combines two chip solution into one. Other than that it also added always-on and constant tsc and lapic timers. Medfield is the platform name, and the chip name is called Penwell we treat Medfield/Penwell as a variant of Moorestown. Penwell can be identified via MSRs.

> Intel MID is Intel's Low Power Intel Architecture (LPIA) based Mobile Internet Device(MID) platform. Unlike standard x86 PCs, Intel MID does not have many legacy devices nor standard legacy replacement devices/features. e.g. It does not contain i8259, i8254, HPET, legacy BIOS, most of the io ports.

    x86 Intel MID Platform
    bcm43340
    Medfield MID Platform
    Intel MID Platform

arch/x86/Kconfig

    if X86_WANT_INTEL_MID
    config X86_INTEL_MID
    bool "Intel MID Platform"
       depends on PCI
       depends on PCI_GOANY
       depends on X86_IO_APIC
       select X86_INTEL_MID
       select SFI
       select INTEL_SCU_IPC
       select X86_PLATFORM_DEVICES
       select ARCH_HAVE_CUSTOM_GPIO_H
    
    config X86_MDFLD
    bool "Medfield MID platform"
       depends on X86_INTEL_MID
       select DW_APB_TIMER
       select APB_TIMER
       select I2C
       select SPI
       select INTEL_SCU_IPC
       select X86_PLATFORM_DEVICES
       select MFD_INTEL_MSIC
    
    config ATOM_SOC_POWER
    bool "Select Atom SOC Power"
    
    config INTEL_DEBUG_FEATURE
    bool "Debug feature interface on Intel MID platform"
       depends on X86_INTEL_MID
       Provides an interface to list the debug features
        that are enabled on an Intel MID platform. The
        enabling of the debug features depends on the mode
        the device is in (e.g. manufacturing, production,
        end user, etc...).

    config ARCH_NR_GPIO
       depends on ARCH_HAVE_CUSTOM_GPIO_H
       default 512 if X86_INTEL_MID
       default 0
        Maximum number of GPIOs in the system.

arch/x86/Kconfig.cpu

    config MSLM
           bool "Intel Silvermont (Atom)"
           ---help---
    
             Select this for the Intel Silvermont (Atom) platform. Intel Atom
             CPUs have an in-order pipelining architecture and thus can benefit
             from accordingly optimized code. Use a recent GCC with specific
             Atom support in order to fully benefit from selecting this option.
    
    X86_L1_CACHE_SHIFT
    X86_USE_PPRO_CHECKSUM
    X86_TSC
    X86_CMPXCHG64
    X86_CMOV
    
arch/x86/Makefile_32.cpu

            cflags-$(CONFIG_MSLM) += $(call cc-option,-march=slm) \
                $(call cc-option,-mtune=slm,$(call cc-option,-mtune=generic))

### Platform

#### Intel MID Specific Setup Code

    arch/x86/include/asm/intel-mid.h

It includes code from:

- SFI
- PCI
- Platform Device
- GPIO
- OEMB Table
- IAFW
- Device Creation (Board Information)
- x86_init, x86_platform_init


    #define INTEL_MID_OPS_INIT {\
           DECLARE_INTEL_MID_OPS_INIT(penwell, INTEL_MID_CPU_CHIP_PENWELL) \
           DECLARE_INTEL_MID_OPS_INIT(cloverview, INTEL_MID_CPU_CHIP_CLOVERVIEW) \
           DECLARE_INTEL_MID_OPS_INIT(tangier, INTEL_MID_CPU_CHIP_TANGIER) \

Related

    arch/x86/include/asm/intel_mid_gpadc.h
    arch/x86/include/asm/intel_mid_hsu.h
    arch/x86/include/asm/intel_mid_pcihelpers.h
    arch/x86/include/asm/intel_mid_powerbtn.h
    arch/x86/include/asm/intel_mid_pwm.h
    arch/x86/include/asm/intel_mid_remoteproc.h INTEL MID Remote Processor 
    arch/x86/include/asm/intel_mid_rpmsg.h
    arch/x86/include/asm/intel_mid_thermal.h
      SoC level power limits for thermal throttling
      intel mid thermal driver
    arch/x86/include/asm/module.h
      elif (defined CONFIG_MATOM) || (defined CONFIG_MSLM)
    arch/x86/include/asm/required-features.h
      if defined(CONFIG_MATOM) || defined(CONFIG_MSLM)
    arch/x86/include/asm/setup.h
      extern void x86_intel_mid_early_setup(void);
      static inline void x86_intel_mid_early_setup(void) { }
    arch/x86/include/uapi/asm/bootparam.h
    arch/x86/include/uapi/asm/msr-index.h
    arch/x86/kernel/cpu/common.c
    arch/x86/kernel/cpu/intel.c
      case 0x4A:      /* Merrifield */
    arch/x86/kernel/cpu/mcheck/therm_throt.c
    arch/x86/kernel/early_printk.c
    arch/x86/kernel/head32.c
      case X86_SUBARCH_INTEL_MID:
    arch/x86/kernel/irq.c
    arch/x86/kernel/rtc.c
    arch/x86/kernel/smpboot.c
    arch/x86/pci/mrst.c
    arch/x86/platform/Makefile
      obj-y  += intel-mid/
    arch/x86/platform/intel-mid/Makefile
      Very Important!
    arch/x86/platform/intel-mid/board.c | Intel Medfield based board (Blackbay)
      Very Important!
    arch/x86/platform/intel-mid/device_libs/Makefile
    arch/x86/platform/intel-mid/device_libs/pci/platform_sdhci_pci.c | mmc sdhci pci platform data initilization file
    arch/x86/platform/intel-mid/device_libs/pci/platform_sdhci_pci.h
    arch/x86/platform/intel-mid/device_libs/pci/platform_usb_otg.c | USB OTG platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_ads7955.c | ads7955 platform data initialization file
    arch/x86/platform/intel-mid/device_libs/platform_ads7955.h
    arch/x86/platform/intel-mid/device_libs/platform_bq24261.c | Platform data for bq24261 charger driver
    arch/x86/platform/intel-mid/device_libs/platform_bq24261.h
    arch/x86/platform/intel-mid/device_libs/platform_emc1403.c | emc1403 platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_emc1403.h
    arch/x86/platform/intel-mid/device_libs/platform_lis331.c | lis331 platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_lis331.h
    arch/x86/platform/intel-mid/device_libs/platform_max3111.c | max3111 platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_max3111.h
    arch/x86/platform/intel-mid/device_libs/platform_max7315.c | max7315 platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_max7315.h
    arch/x86/platform/intel-mid/device_libs/platform_mid_pwm.c | mid_pwm platform data initilization file
      PWM_LED
      PWM_VIBRATOR
      PWM_LCD_BACKLIGHT
    arch/x86/platform/intel-mid/device_libs/platform_mid_pwm.h
    arch/x86/platform/intel-mid/device_libs/platform_mpu3050.c | mpu3050 platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_mpu3050.h
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_ocd.c | Platform data for Merrifield Platform OCD  Driver
      +#include <asm/intel-mid.h>
      +#include <asm/intel_mid_remoteproc.h>
      +#include <asm/intel_scu_ipc.h>
      +#include <asm/intel_basincove_ocd.h>
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_ocd.h
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_thermal.c | Intel Merrifield Platform thermal driver
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_thermal.h
    arch/x86/platform/intel-mid/device_libs/platform_msic.c | MSIC platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic.h
    arch/x86/platform/intel-mid/device_libs/platform_msic_adc.c | MSIC ADC platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic_adc.h
    arch/x86/platform/intel-mid/device_libs/platform_msic_audio.c | MSIC audio platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic_audio.h
    arch/x86/platform/intel-mid/device_libs/platform_msic_battery.c | MSIC battery platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic_battery.h
    arch/x86/platform/intel-mid/device_libs/platform_msic_gpio.c | MSIC GPIO platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic_gpio.h
    arch/x86/platform/intel-mid/device_libs/platform_msic_ocd.c | MSIC OCD platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic_ocd.h
    arch/x86/platform/intel-mid/device_libs/platform_msic_power_btn.c | MSIC power btn platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic_power_btn.h
    arch/x86/platform/intel-mid/device_libs/platform_msic_thermal.c | msic_thermal platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_msic_thermal.h
    arch/x86/platform/intel-mid/device_libs/platform_pcal9555a.c | pcal9555a platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_pcal9555a.h
    arch/x86/platform/intel-mid/device_libs/platform_pmic_gpio.c | PMIC GPIO platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_pmic_gpio.h
    arch/x86/platform/intel-mid/device_libs/platform_scu_flis.c | scu_flis platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_scu_flis.h
    arch/x86/platform/intel-mid/device_libs/platform_sdio_regulator.c | sdio regulator platform device initilization file
    arch/x86/platform/intel-mid/device_libs/platform_soc_thermal.c | Platform data for SoC DTS driver
    arch/x86/platform/intel-mid/device_libs/platform_soc_thermal.h
    arch/x86/platform/intel-mid/device_libs/platform_spidev.c | spidev platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_spidev.h
    arch/x86/platform/intel-mid/device_libs/platform_tc35876x.c | tc35876x platform data initilization file
    arch/x86/platform/intel-mid/device_libs/platform_tc35876x.h
    arch/x86/platform/intel-mid/device_libs/platform_tca6416.c | tca6416 platform data initilization file
    Here

### APIC

    arch/x86/kernel/apic/apic.c
    arch/x86/kernel/apic/io_apic.c

### APB Timer

> Langwell is the south complex of Intel Moorestown MID platform. There are eight external timers in total that can be used by the operating system. The timer information, such as frequency and addresses, is provided to the OS via SFI tables. 

> Timer interrupts are routed via FW/HW emulated IOAPIC independently via individual redirection table entries (RTE). Unlike HPET, there is no master counter, therefore one of the timers are used as clocksource. The overall allocation looks like:
- timer 0 - NR_CPUs for per cpu timer
- one timer for clocksource
- one timer for watchdog driver.

> It is also worth notice that APB timer does not support true one-shot mode, free-running mode will be used here to emulate one-shot mode. APB timer can also be used as broadcast timer along with per cpu local APIC timer, but by default APB timer has higher rating than local APIC timers.


    arch/x86/kernel/apb_timer.c | Driver for Langwell APB timers

 
### Power

    arch/x86/include/asm/mwait.h
      +#ifdef CONFIG_ATOM_SOC_POWER
      +#define MWAIT_MAX_NUM_CSTATES          10
      +#else
      +#define MWAIT_MAX_NUM_CSTATES          8
      +#endif
    arch/x86/include/asm/pmic_pdata.h
      pmic_platform_data
      #ifdef CONFIG_PMIC_CCSM
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_pmic.c | latform data for Merrifield PMIC driver
      #include <linux/sfi.h>
      #include <linux/power/bq24261_charger.h>
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_pmic.h | platform data for pmic driver
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_pmic_i2c.c | Platform data for Merrifield PMIC I2C
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_pmic_i2c.h
    arch/x86/platform/intel-mid/device_libs/platform_mrfl_regulator.c



### Debug

    arch/x86/include/asm/intel_soc_debug.h

### MIP

    arch/x86/include/asm/intel_mip.h

### SCU IPC

> The IPC is used to bridge the communications between kernel and SCU on some embedded Intel x86 platforms.

> Driver for the Intel SCU IPC mechanism

> SCU runing in ARC processor communicates with other entity running in IA core through IPC mechanism which in turn messaging between IA core ad SCU. SCU has two IPC mechanism IPC-1 and IPC-2. IPC-1 is used between IA32 and SCU where IPC-2 is used between P-Unit and SCU. This driver delas with IPC-1 Driver provides an API for power control unit registers (e.g. MSIC) along with other APIs.

    obj-$(CONFIG_INTEL_SCU_IPC)	+= intel_scu_ipc.o
    arch/x86/Kconfig | Not Edison Patch 
    arch/x86/include/asm/intel_scu_ipc.h | Not Edison Patch 
    arch/x86/kernel/Makefile | Not Edison Patch 
    arch/x86/kernel/intel_scu_ipc.c | Not Edison Patch
    
    arch/x86/include/asm/intel_scu_flis.h | SCU FLIS Interfaces
    arch/x86/include/asm/intel_scu_ipc.h
    arch/x86/include/asm/intel_scu_ipcutil.h
    arch/x86/include/asm/intel_scu_pmic.h
    arch/x86/include/asm/scu_ipc_rpmsg.h
    
    arch/x86/platform/intel-mid/device_libs/platform_ipc.c | IPC platform library file
    arch/x86/platform/intel-mid/device_libs/platform_ipc.h
    
    
    OSHOB-OS Handoff Buffer
    OSNIB interface
    scu_ipc_pmdb_buffer

### Virtual Real Time Clock (VRTC)

> VRTC is emulated by system controller firmware, the real HW RTC is located in the PMIC device. SCU FW shadows PMIC RTC in a memory mapped IO space that is visible to the host IA processor. This driver is based on RTC CMOS driver.

> Moorestown platform doesn't have a m146818 RTC device like traditional x86 PC, but a firmware emulated virtual RTC device(vrtc), which provides some basic RTC functions like get/set time. vrtc serves as the only wall clock device on Moorestown platform.

> Currently, vrtc init func will be called as arch_initcall() before xtime's init. Also move the sfi vrtc table parsing from mrst.c to vrtc.c

There will be another general vrtc driver for rtc subsystem

    arch/x86/include/asm/intel_mid_vrtc.h
    
    obj-$(CONFIG_X86_MRST)		+= mrst.o vrtc.o
    arch/x86/include/asm/fixmap.h
    arch/x86/include/asm/vrtc.h
    arch/x86/kernel/mrst.c
    arch/x86/kernel/vrtc.c
    arch/x86/platform/mrst/vrtc.c | Driver for virtual RTC device on Intel MID platform
    

### HSU

> Intel Medfield platform has a high speed UART device, which could act as a early console. To enable early printk of HSU console, simply add "earlyprintk=hsu" in kernel command line. Currently we put the code in the early_printk_mrst.c as it is also for Intel MID platforms like the mrst early console

Upstream patch

- arch/x86/include/asm/intel_mid_hsu.h
- arch/x86/include/asm/mrst.h
- arch/x86/kernel/early_printk.c
- arch/x86/kernel/early_printk_mrst.c
- include/linux/platform_data/dma-hsu.h | Changes for High Speed UART DMA
- drivers/dma/hsu/hsu.c
- drivers/dma/hsu/pci.c
- drivers/external_drivers/drivers/hsu/mfd_pci.c

It includes enums from:

- hsu_port0
- hsu_port1
- hsu_port2
- bt_port
- modem_port
- gps_port
- debug_port
- hsu_intel
- hsu_dw

- arch/x86/platform/intel-mid/device_libs/platform_hsu.c
- arch/x86/platform/intel-mid/device_libs/platform_hsu.h

- https://communities.intel.com/thread/75472
- https://lkml.org/lkml/2010/9/13/33

### Basin Cove GPADC

> GPADC(General Purpose Analog Digital Converter)

    config BASINCOVE_GPADC
    depends on INTEL_SCU_IPC

- Platform data for Merrifield Basincove GPADC driver
- Intel Merrifield Basin Cove GPADC Driver
- BASINCOVE GPADC driver for Intel Merrifield platform


    arch/x86/include/asm/intel_basincove_gpadc.h
    arch/x86/platform/intel-mid/device_libs/platform_bcove_adc.c
    arch/x86/platform/intel-mid/device_libs/platform_bcove_adc.h
    
    drivers/iio/adc/iio_basincove_gpadc.c


Related

    ACPI / PMIC: support PMIC operation region for CrystalCove
    #define DRIVER_NAME "bcove_bcu"
    #define DEVICE_NAME "mrfl_pmic_bcu"

arch/x86/include/asm/intel_basincove_gpadc.h
arch/x86/include/asm/intel_basincove_ocd.h

### BlueTooth

Broadcom Bluetooth Low Power Mode
    
    bcm_bt_lpm


    arch/x86/include/asm/bcm_bt_lpm.h
    drivers/misc/bcm-bt-lpm.c
    arch/x86/platform/intel-mid/device_libs/platform_btlpm.c | btlpm platform data initialization file
      Bluetooth is using UART port number 0
      .name = "bcm_bt_lpm",
      device_initcall(bluetooth_init);

### GPIO
arch/x86/include/asm/gpio.h

### GPIO Keys

> We will search these buttons in SFI GPIO table (by name) and register them dynamically. Please add all possible buttons here, we will shrink them if no GPIO found.

    arch/x86/platform/intel-mid/device_libs/platform_gpio_keys.c
      late_initcall(pb_keys_init);
    arch/x86/platform/intel-mid/device_libs/platform_gpio_keys.h

### I2C

arch/x86/platform/intel-mid/device_libs/platform_dw_i2c.c | I2C platform data initilization file


### SFI

config CONFIG_SFI

## Modules

root@edison:~/InternetOfThings101# lsmod
Module                  Size  Used by
usb_f_acm              14335  1 
u_serial               18582  6 usb_f_acm
g_multi                70924  0 
libcomposite           39245  2 usb_f_acm,g_multi
bcm_bt_lpm             13708  0 
bcm4334x              587105  0 

    
https://www.broadcom.com/products/wireless-connectivity/bluetooth/bcm43341

    Documentation/kernel-parameters.txt
    arch/x86/configs/i386_edison_defconfig
    arch/x86/
    arch/x86/platform/intel-mid/
    arch/x86/platform/mrst/
    drivers/acpi/
    drivers/bluetooth/
    drivers/cpufreq/
    drivers/dma/
    drivers/gpio/
    drivers/hwmon/intel_mcu_common.c
    drivers/hwmon/intel_mcu_common.h
    drivers/hwmon/intel_mid_gpadc.c
    drivers/i2c/busses/
    drivers/idle/
    drivers/iio/adc/
    drivers/iio/adc/iio_basincove_gpadc.c
    drivers/iio/adc/ti-ads7955.c
    drivers/misc/bcm-lpm/bcm_bt_lpm.c
    drivers/misc/emmc_ipanic.c
    drivers/misc/pti.c
    drivers/misc/stm.c
    drivers/misc/stm.h
    drivers/mmc/card/block.c
    drivers/mmc/core/
    drivers/mmc/host/
    drivers/net/wireless/
    drivers/pci/pci-atom_soc.c
    drivers/platform/x86/
    drivers/pci/pci-atom_soc.c
    drivers/pci/pci.c
    drivers/pci/quirks.c
    drivers/platform/x86/Kconfig
    drivers/platform/x86/Makefile
    drivers/platform/x86/intel_mid_powerbtn.c
    drivers/platform/x86/intel_mid_thermal.c
    drivers/platform/x86/intel_pmic_gpio.c
    drivers/platform/x86/intel_psh_ipc.c
    drivers/platform/x86/intel_scu_flis.c
    drivers/platform/x86/intel_scu_fw_update.c
    drivers/platform/x86/intel_scu_ipc.c
    drivers/platform/x86/intel_scu_ipcutil.c
    drivers/platform/x86/intel_scu_mip.c
    drivers/platform/x86/intel_scu_pmic.c
    drivers/power/
    drivers/pwm/
    drivers/regulator/
    drivers/remoteproc/
    drivers/rpmsg/
    drivers/rtc/
    drivers/spi/
    drivers/thermal/
    drivers/tty/serial/
    drivers/usb/core/
    drivers/usb/dwc3/
    drivers/usb/gadget/
    drivers/usb/host/
    drivers/watchdog/
    net/bluetooth/l2cap_core.c
    sound/core/
    sound/soc/
    sound/soc/codecs/sn95031.c
    sound/soc/codecs/wm8994.c
    sound/soc/codecs/wm_hubs.c
    sound/soc/intel/

## Kernel Interfaces

### SFI Simple Firmware Interface

http://www.h-online.com/open/news/item/Intel-develops-simpler-alternative-to-ACPI-for-Linux-742161.html

> How does SFI relate to ACPI? While some modern platforms can used SFI instead of using ACPI, SFI is not intended to replace ACPI on general purpose systems. If a platform were to export both SFI and ACPI booted an OS that also supports both, the OS should use the platform's ACPI support and ignore SFI.
    
- https://en.wikipedia.org/wiki/Simple_Firmware_Interface
- https://simplefirmware.org/
- https://www.kernel.org/doc/ols/2009/ols2009-pages-55-60.pdf
- https://lwn.net/Articles/406228/
- https://simplefirmware.org/faq


http://geektimes.ru/post/255136/
https://communities.intel.com/message/273743
https://edison.internet-share.com/w/index.php?title=Using_a_stock_Linux_kernel_with_Intel_Edison&redirect=no

User Linux Next
git clone git://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git
v4.1-rc6 tag, mrproper'd and rebuilt, 

root@edison:~# dmesg
[    0.000000] Initializing cgroup subsys cpuset
[    0.000000] Initializing cgroup subsys cpu
[    0.000000] Initializing cgroup subsys cpuacct
[    0.000000] Linux version 3.10.17-poky-edison+ (sys_dswci@tlsndgbuild004) (gcc version 4.9.1 (GCC) ) #1 SMP PREEMPT Fr5
[    0.000000] e820: BIOS-provided physical RAM map:
[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x0000000000097fff] usable
[    0.000000] BIOS-e820: [mem 0x0000000000100000-0x0000000003ffffff] usable
[    0.000000] BIOS-e820: [mem 0x0000000004000000-0x0000000005ffffff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000006000000-0x000000003f4fffff] usable
[    0.000000] BIOS-e820: [mem 0x000000003f500000-0x000000003fffffff] reserved
[    0.000000] BIOS-e820: [mem 0x00000000fec00000-0x00000000fec00fff] reserved
[    0.000000] BIOS-e820: [mem 0x00000000fec04000-0x00000000fec07fff] reserved
[    0.000000] BIOS-e820: [mem 0x00000000fee00000-0x00000000fee00fff] reserved
[    0.000000] BIOS-e820: [mem 0x00000000ff000000-0x00000000ffffffff] reserved
[    0.000000] NX (Execute Disable) protection: active
[    0.000000] SMBIOS 2.6 present.
[    0.000000] DMI: Intel Corporation Merrifield/BODEGA BAY, BIOS 542 2015.01.21:18.19.48
[    0.000000] e820: update [mem 0x00000000-0x00000fff] usable ==> reserved
[    0.000000] e820: remove [mem 0x000a0000-0x000fffff] usable
[    0.000000] e820: last_pfn = 0x3f500 max_arch_pfn = 0x1000000
[    0.000000] MTRR default type: uncachable
[    0.000000] MTRR fixed ranges enabled:
[    0.000000]   00000-9FFFF write-back
[    0.000000]   A0000-BFFFF uncachable
[    0.000000]   C0000-FFFFF write-back
[    0.000000] MTRR variable ranges enabled:
[    0.000000]   0 base 000000000 mask FC0000000 write-back
[    0.000000]   1 base 03F600000 mask FFFE00000 uncachable
[    0.000000]   2 base 03F800000 mask FFF800000 uncachable
[    0.000000]   3 base 004000000 mask FFE000000 uncachable
[    0.000000]   4 disabled
[    0.000000]   5 disabled
[    0.000000]   6 disabled
[    0.000000]   7 disabled
[    0.000000] x86 PAT enabled: cpu 0, old 0x7040600070406, new 0x7010600070106
[    0.000000] original variable MTRRs
[    0.000000] reg 0, base: 0GB, range: 1GB, type WB
[    0.000000] reg 1, base: 1014MB, range: 2MB, type UC
[    0.000000] reg 2, base: 1016MB, range: 8MB, type UC
[    0.000000] reg 3, base: 64MB, range: 32MB, type UC
[    0.000000] total RAM covered: 982M
[    0.000000] Found optimal setting for mtrr clean up
[    0.000000]  gran_size: 64K  chunk_size: 512M        num_reg: 5      lose cover RAM: 0G
[    0.000000] New variable MTRRs
[    0.000000] reg 0, base: 0GB, range: 512MB, type WB
[    0.000000] reg 1, base: 64MB, range: 32MB, type UC
[    0.000000] reg 2, base: 512MB, range: 512MB, type WB
[    0.000000] reg 3, base: 1014MB, range: 2MB, type UC
[    0.000000] reg 4, base: 1016MB, range: 8MB, type UC
[    0.000000] e820: update [mem 0x04000000-0x05ffffff] usable ==> reserved
[    0.000000] initial memory mapped: [mem 0x00000000-0x023fffff]
[    0.000000] Base memory trampoline at [c0094000] 94000 size 16384
[    0.000000] init_memory_mapping: [mem 0x00000000-0x000fffff]
[    0.000000]  [mem 0x00000000-0x000fffff] page 4k
[    0.000000] init_memory_mapping: [mem 0x37800000-0x379fffff]
[    0.000000]  [mem 0x37800000-0x379fffff] page 2M
[    0.000000] init_memory_mapping: [mem 0x34000000-0x377fffff]
[    0.000000]  [mem 0x34000000-0x377fffff] page 2M
[    0.000000] init_memory_mapping: [mem 0x00100000-0x03ffffff]
[    0.000000]  [mem 0x00100000-0x001fffff] page 4k
[    0.000000]  [mem 0x00200000-0x03ffffff] page 2M
[    0.000000] init_memory_mapping: [mem 0x06000000-0x33ffffff]
[    0.000000]  [mem 0x06000000-0x33ffffff] page 2M
[    0.000000] init_memory_mapping: [mem 0x37a00000-0x37bfdfff]
[    0.000000]  [mem 0x37a00000-0x37bfdfff] page 4k
[    0.000000] BRK [0x01e27000, 0x01e27fff] PGTABLE
[    0.000000] 121MB HIGHMEM available.
[    0.000000] 891MB LOWMEM available.
[    0.000000]   mapped low ram: 0 - 37bfe000
[    0.000000]   low ram: 0 - 37bfe000
[    0.000000] BRK [0x01e28000, 0x01e28fff] PGTABLE
[    0.000000] Zone ranges:
[    0.000000]   DMA      [mem 0x00001000-0x00ffffff]
[    0.000000]   Normal   [mem 0x01000000-0x37bfdfff]
[    0.000000]   HighMem  [mem 0x37bfe000-0x3f4fffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x00001000-0x00097fff]
[    0.000000]   node   0: [mem 0x00100000-0x03ffffff]
[    0.000000]   node   0: [mem 0x06000000-0x3f4fffff]
[    0.000000] On node 0 totalpages: 251031
[    0.000000] free_area_init_node: node 0, pgdat c1c59e40, node_mem_map f740e020
[    0.000000]   DMA zone: 32 pages used for memmap
[    0.000000]   DMA zone: 0 pages reserved
[    0.000000]   DMA zone: 3991 pages, LIFO batch:0
[    0.000000]   Normal zone: 1752 pages used for memmap
[    0.000000]   Normal zone: 216062 pages, LIFO batch:31
[    0.000000]   HighMem zone: 243 pages used for memmap
[    0.000000]   HighMem zone: 30978 pages, LIFO batch:7
[    0.000000] Using APIC driver default
[    0.000000] SFI: Simple Firmware Interface v0.81 http://simplefirmware.org
[    0.000000] SFI: SYST E31F0, 0060 (v1  INTEL INTELFDK)
[    0.000000] SFI: CPUS E3296, 0020 (v1  INTEL INTELFDK)
[    0.000000] SFI: FREQ E32C2, 0030 (v1  INTEL INTELFDK)
[    0.000000] SFI: MMAP E32FE, 01A4 (v1  INTEL INTELFDK)
[    0.000000] SFI: XSDT E34B0, 002C (v1  INTEL INTELFDK)
[    0.000000] SFI: APIC E353E, 0020 (v1  INTEL INTELFDK)
[    0.000000] SFI: WAKE E356A, 0020 (v2  INTEL INTELFDK)
[    0.000000] SFI: DEVS E359E, 047D (v1  INTEL INTELFDK)
[    0.000000] SFI: GPIO E3A27, 0964 (v1  INTEL INTELFDK)
[    0.000000] SFI: OEMB E4397, 0060 (v5 UMGFDK CFGINFO!)
[    0.000000] SFI: registering lapic[0]
[    0.000000] SFI: registering lapic[2]
[    0.000000] IOAPIC[0]: apic_id 0, version 32, address 0xfec00000, GSI 0-54
[    0.000000] smpboot: Allowing 2 CPUs, 0 hotplug CPUs
[    0.000000] nr_irqs_gsi: 71
[    0.000000] e820: [mem 0x40000000-0xfebfffff] available for PCI devices
[    0.000000] setup_percpu: NR_CPUS:2 nr_cpumask_bits:2 nr_cpu_ids:2 nr_node_ids:1
[    0.000000] PERCPU: Embedded 14 pages/cpu @f73e8000 s33856 r0 d23488 u57344
[    0.000000] pcpu-alloc: s33856 r0 d23488 u57344 alloc=14*4096
[    0.000000] pcpu-alloc: [0] 0 [0] 1 
[    0.000000] Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 249247
[    0.000000] Kernel command line: rootwait root=PARTUUID=012b3303-34ac-284d-99b4-34e03a2335f4 rootfstype=ext4 console=ty
[    0.000000] PID hash table entries: 4096 (order: 2, 16384 bytes)
[    0.000000] Dentry cache hash table entries: 131072 (order: 7, 524288 bytes)
[    0.000000] Inode-cache hash table entries: 65536 (order: 6, 262144 bytes)
[    0.000000] Initializing CPU#0
[    0.000000] Initializing HighMem for node 0 (00037bfe:0003f500)
[    0.000000] Memory: 982520k/1037312k available (7064k kernel code, 21604k reserved, 3679k data, 572k init, 123912k hig)
[    0.000000] virtual kernel memory layout:
[    0.000000]     fixmap  : 0xfff8b000 - 0xfffff000   ( 464 kB)
[    0.000000]     pkmap   : 0xffc00000 - 0xffe00000   (2048 kB)
[    0.000000]     vmalloc : 0xf83fe000 - 0xffbfe000   ( 120 MB)
[    0.000000]     lowmem  : 0xc0000000 - 0xf7bfe000   ( 891 MB)
[    0.000000]       .init : 0xc1c7e000 - 0xc1d0d000   ( 572 kB)
[    0.000000]       .data : 0xc18e60e0 - 0xc1c7dfc0   (3679 kB)
[    0.000000]       .text : 0xc1200000 - 0xc18e60e0   (7064 kB)
[    0.000000] Checking if this processor honours the WP bit even in supervisor mode...Ok.
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=2, Nodes=1
[    0.000000] Preemptible hierarchical RCU implementation.
[    0.000000]  Additional per-CPU info printed with stalls.
[    0.000000] NR_IRQS:2304 nr_irqs:512 16
[    0.000000] CPU 0 irqstacks, hard=f6c08000 soft=f6c0a000
[    0.000000] Console: colour dummy device 80x25
[    0.000000] kmemleak: Kernel memory leak detector disabled
[    0.000000] tsc: Detected 499.200 MHz processor
[    0.000008] Calibrating delay loop (skipped), value calculated using timer frequency.. 998.40 BogoMIPS (lpj=4992000)
[    0.000031] pid_max: default: 32768 minimum: 301
[    0.000261] Security Framework initialized
[    0.000289] SELinux:  Initializing.
[    0.000351] SELinux:  Starting in permissive mode
[    0.000431] Mount-cache hash table entries: 512
[    0.001587] Initializing cgroup subsys devices
[    0.001612] Initializing cgroup subsys freezer
[    0.001630] Initializing cgroup subsys blkio
[    0.001646] Initializing cgroup subsys perf_event
[    0.001788] CPU: Physical Processor ID: 0
[    0.001804] CPU: Processor Core ID: 0
[    0.001822] ENERGY_PERF_BIAS: Set to 'normal', was 'performance'
[    0.001822] ENERGY_PERF_BIAS: View and update with x86_energy_perf_policy(8)
[    0.001843] mce: CPU supports 6 MCE banks
[    0.001874] CPU0: Thermal monitoring enabled (TM1)
[    0.001917] Last level iTLB entries: 4KB 0, 2MB 0, 4MB 0
[    0.001917] Last level dTLB entries: 4KB 128, 2MB 0, 4MB 0
[    0.001917] tlb_flushall_shift: 6
[    0.002345] Freeing SMP alternatives: 28k freed
[    0.002400] SFI: MCFG E34F6, 003C (v1  INTEL INTELFDK)
[    0.002419] ftrace: allocating 28044 entries in 55 pages
[    0.069742] Enabling APIC mode:  Flat.  Using 1 I/O APICs
[    0.069821] smpboot: CPU0: Genuine Intel(R) CPU   4000  @  500MHz (fam: 06, model: 4a, stepping: 08)
[    0.069870] TSC deadline timer enabled
[    0.069931] Performance Events: no PEBS fmt2+, generic architected perfmon, Intel PMU driver.
[    0.069976] ... version:                3
[    0.069990] ... bit width:              40
[    0.070002] ... generic registers:      2
[    0.070015] ... value mask:             000000ffffffffff
[    0.070028] ... max period:             000000007fffffff
[    0.070039] ... fixed-purpose events:   3
[    0.070052] ... event mask:             0000000700000003
[    0.110411] ftrace: Allocated trace_printk buffers
[    0.161434] CPU 1 irqstacks, hard=f6f8c000 soft=f6f8e000
[    0.161455] smpboot: Booting Node   0, Processors  #1 OK
[    0.171664] Initializing CPU#1
[    0.172625] Skipped synchronization checks as TSC is reliable.
[    0.173078] NMI watchdog: enabled on all CPUs, permanently consumes one hw-PMU counter.
[    0.173160] Brought up 2 CPUs
[    0.173181] smpboot: Total of 2 processors activated (1996.80 BogoMIPS)
[    0.175122] devtmpfs: initialized
[    0.185960] SFI: SFI sysfs interfaces init success
[    0.186543] regulator-dummy: no parameters
[    0.187041] NET: Registered protocol family 16
[    0.189137] SFI OEMB Layout
[    0.189175]  OEMB signature               : OEMB
[    0.189175]  OEMB length                  : 96
[    0.189175]  OEMB revision                : 5
[    0.189175]  OEMB checksum                : 0x8D
[    0.189175]  OEMB oem_id                  : UMGFDK
[    0.189175]  OEMB oem_table_id            : CFGINFO!
[    0.189175]  OEMB board_id                : 0x02
[    0.189175]  OEMB iafw version            : 002.012
[    0.189175]  OEMB val_hooks version       : 002.004
[    0.189175]  OEMB ia suppfw version       : 000.000
[    0.189175]  OEMB scu runtime version     : 176.073
[    0.189175]  OEMB ifwi version            : 237.015
[    0.189276] intel_soc_thermal: IPC bus = 0, name =         soc_thrm, irq = 0x 1
[    0.189493] IPC bus, name =        bcove_adc, irq = 0x32
[    0.189694] IPC bus, name =       bcove_thrm, irq = 0x34
[    0.189904] IPC bus, name =  bcove_power_btn, irq = 0x1e
[    0.190076] IPC bus, name =        pmic_ccsm, irq = 0x1b
[    0.190319] SDIO bus = 1, name = bcm43xx_clk_vmmc, ref_clock = 26000000, addr =0x401
[    0.190335] Using generic wifi platform data
[    0.190351] wifi_platform_data: GPIO == 64
[    0.190497] IPC bus, name =        msic_gpio, irq = 0x31
[    0.190677] I2C bus = 1, name =      pcal9555a-1, irq = 0x 0, addr = 0x20
[    0.190713] I2C bus = 1, name =      pcal9555a-2, irq = 0x 0, addr = 0x21
[    0.190745] I2C bus = 1, name =      pcal9555a-3, irq = 0x 0, addr = 0x22
[    0.190776] I2C bus = 1, name =      pcal9555a-4, irq = 0x 0, addr = 0x23
[    0.190808] SPI bus=5, name=         ads7955, irq=0x 0, max_freq=20000000, cs=0
[    0.190831] SPI bus=5, name=          spidev, irq=0x 0, max_freq=25000000, cs=1
[    0.190851] IPC bus, name =        mrfld_sst, irq = 0xff
[    0.191130] pgrr = 000003d5
[    0.191606] PCI: MMCONFIG for domain 0000 [bus 00-00] at [mem 0x3f500000-0x3f5fffff] (base 0x3f500000)
[    0.191631] PCI: MMCONFIG at [mem 0x3f500000-0x3f5fffff] reserved in E820
[    0.191644] PCI: Using MMCONFIG for extended config space
[    0.191658] PCI: Using configuration type 1 for base access
[    0.204921] bio: create slab <bio-0> at 0
[    0.206248] vgaarb: loaded
[    0.206926] SCSI subsystem initialized
[    0.207321] usbcore: registered new interface driver usbfs
[    0.207419] usbcore: registered new interface driver hub
[    0.207626] usbcore: registered new device driver usb
[    0.207911] media: Linux media interface: v0.10
[    0.208001] Linux video capture interface: v2.00
[    0.208075] pps_core: LinuxPPS API ver. 1 registered
[    0.208090] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.208130] PTP clock support registered
[    0.208630]  remoteproc0: intel_rproc_scu is available
[    0.208649]  remoteproc0: Note: remoteproc is still under development and considered experimental.
[    0.208664]  remoteproc0: THE BINARY FORMAT IS NOT YET FINALIZED, and backward compatibility isn't yet guaranteed.
[    0.209075]  remoteproc0: registered virtio0 (type 7)
[    0.209325]  remoteproc0: powering up intel_rproc_scu
[    0.209353]  remoteproc0: Booting fw image intel_mid/intel_mid_remoteproc.fw, size 4456
[    0.209392] Started intel scu remote processor
[    0.209410]  remoteproc0: remote processor intel_rproc_scu is now up
[    0.209759] virtio_rpmsg_bus virtio0: creating channel rpmsg_bcove_adc addr 0x24
[    0.209950] virtio_rpmsg_bus virtio0: creating channel rpmsg_mrfl_thermal addr 0x25
[    0.210120] virtio_rpmsg_bus virtio0: creating channel rpmsg_mid_powerbtn addr 0x10
[    0.210289] virtio_rpmsg_bus virtio0: creating channel rpmsg_pmic_ccsm addr 0x19
[    0.210456] virtio_rpmsg_bus virtio0: creating channel rpmsg_msic_gpio addr 0x5
[    0.210633] virtio_rpmsg_bus virtio0: creating channel rpmsg_ipc_command addr 0xa0
[    0.210800] virtio_rpmsg_bus virtio0: creating channel rpmsg_ipc_simple_command addr 0xa1
[    0.210967] virtio_rpmsg_bus virtio0: creating channel rpmsg_ipc_raw_command addr 0xa2
[    0.211145] virtio_rpmsg_bus virtio0: creating channel rpmsg_pmic addr 0xff
[    0.211314] virtio_rpmsg_bus virtio0: creating channel rpmsg_mip addr 0xec
[    0.211482] virtio_rpmsg_bus virtio0: creating channel rpmsg_fw_update addr 0x13
[    0.211662] virtio_rpmsg_bus virtio0: creating channel rpmsg_ipc_util addr 0x12
[    0.211844] virtio_rpmsg_bus virtio0: creating channel rpmsg_flis addr 0xf5
[    0.212015] virtio_rpmsg_bus virtio0: creating channel rpmsg_watchdog addr 0xf8
[    0.212186] virtio_rpmsg_bus virtio0: creating channel rpmsg_umip addr 0x14
[    0.212368] virtio_rpmsg_bus virtio0: creating channel rpmsg_osip addr 0x15
[    0.212540] virtio_rpmsg_bus virtio0: creating channel rpmsg_vrtc addr 0xfa
[    0.212752] virtio_rpmsg_bus virtio0: creating channel rpmsg_fw_logging addr 0x27
[    0.212945] virtio_rpmsg_bus virtio0: creating channel rpmsg_kpd_led addr 0x23
[    0.213124] virtio_rpmsg_bus virtio0: creating channel rpmsg_modem_nvram addr 0xa2
[    0.213301] virtio_rpmsg_bus virtio0: creating channel rpmsg_mid_pwm addr 0x22
[    0.213474] virtio_rpmsg_bus virtio0: rpmsg host is online
[    0.213600] intel_mid_rpmsg rpmsg5: Probed rpmsg_ipc device rpmsg_ipc_command
[    0.213621] intel_mid_rpmsg rpmsg5: Allocating rpmsg_instance
[    0.213677] intel_mid_rpmsg rpmsg6: Probed rpmsg_ipc device rpmsg_ipc_simple_command
[    0.213697] intel_mid_rpmsg rpmsg6: Allocating rpmsg_instance
[    0.213749] intel_mid_rpmsg rpmsg7: Probed rpmsg_ipc device rpmsg_ipc_raw_command
[    0.213769] intel_mid_rpmsg rpmsg7: Allocating rpmsg_instance
[    0.214285] Advanced Linux Sound Architecture Driver Initialized.
[    0.214303] Intel MID platform detected, using MID PCI ops
[    0.214316] PCI: Probing PCI hardware
[    0.214332] PCI: root bus 00: using default resources
[    0.214347] PCI: Probing PCI hardware (bus 00)
[    0.214610] PCI host bridge to bus 0000:00
[    0.214639] pci_bus 0000:00: root bus resource [io  0x0000-0xffff]
[    0.214663] pci_bus 0000:00: root bus resource [mem 0x00000000-0xfffffffff]
[    0.214682] pci_bus 0000:00: No busn resource found for root bus, will use [bus 00-ff]
[    0.214741] pci 0000:00:00.0: [8086:1170] type 00 class 0x060000
[    0.215136] pci 0000:00:01.0: [8086:1190] type 00 class 0x080501
[    0.215206] pci 0000:00:01.0: reg 10: [mem 0xff3fc000-0xff3fc0ff]
[    0.215420] pci 0000:00:01.0: PME# supported from D0 D3hot
[    0.215767] pci 0000:00:01.2: [8086:1190] type 00 class 0x080501
[    0.215835] pci 0000:00:01.2: reg 10: [mem 0xff3fa000-0xff3fa0ff]
[    0.216048] pci 0000:00:01.2: PME# supported from D0 D3hot
[    0.216379] pci 0000:00:01.3: [8086:1190] type 00 class 0x080501
[    0.216447] pci 0000:00:01.3: reg 10: [mem 0xff3fb000-0xff3fb0ff]
[    0.216659] pci 0000:00:01.3: PME# supported from D0 D3hot
[    0.217018] pci 0000:00:02.0: [8086:1182] type 00 class 0x038000
[    0.217087] pci 0000:00:02.0: reg 10: [mem 0xc0000000-0xc1ffffff]
[    0.217149] pci 0000:00:02.0: reg 18: [mem 0x80000000-0x8fffffff]
[    0.217209] pci 0000:00:02.0: reg 20: [io  0x7ff8-0x7fff]
[    0.217633] pci 0000:00:04.0: [8086:1191] type 00 class 0x070002
[    0.217699] pci 0000:00:04.0: reg 10: [mem 0xff010000-0xff01007f]
[    0.217913] pci 0000:00:04.0: PME# supported from D0 D3hot
[    0.218255] pci 0000:00:04.1: [8086:1191] type 00 class 0x070002
[    0.218323] pci 0000:00:04.1: reg 10: [mem 0xff010080-0xff0100ff]
[    0.218536] pci 0000:00:04.1: PME# supported from D0 D3hot
[    0.218878] pci 0000:00:04.2: [8086:1191] type 00 class 0x070002
[    0.218945] pci 0000:00:04.2: reg 10: [mem 0xff010100-0xff01017f]
[    0.219159] pci 0000:00:04.2: PME# supported from D0 D3hot
[    0.219488] pci 0000:00:04.3: [8086:1191] type 00 class 0x070002
[    0.219555] pci 0000:00:04.3: reg 10: [mem 0xff010180-0xff0101ff]
[    0.219768] pci 0000:00:04.3: PME# supported from D0 D3hot
[    0.220123] pci 0000:00:05.0: [8086:1192] type 00 class 0x070002
[    0.220190] pci 0000:00:05.0: reg 10: [mem 0xff010400-0xff0107ff]
[    0.220403] pci 0000:00:05.0: PME# supported from D0 D3hot
[    0.220736] pci 0000:00:06.0: [8086:1193] type 00 class 0x088000
[    0.220804] pci 0000:00:06.0: reg 10: [mem 0xff2a0000-0xff2a0fff]
[    0.221016] pci 0000:00:06.0: PME# supported from D0 D3hot
[    0.221396] pci 0000:00:06.1: [8086:1193] type 00 class 0x088000
[    0.221464] pci 0000:00:06.1: reg 10: [mem 0xff2a1000-0xff2a1fff]
[    0.221677] pci 0000:00:06.1: PME# supported from D0 D3hot
[    0.222037] pci 0000:00:07.0: [8086:1194] type 00 class 0x088000
[    0.222104] pci 0000:00:07.0: reg 10: [mem 0xff188000-0xff188fff]
[    0.222317] pci 0000:00:07.0: PME# supported from D0 D3hot
[    0.222654] pci 0000:00:07.1: [8086:1194] type 00 class 0x088000
[    0.222722] pci 0000:00:07.1: reg 10: [mem 0xff189000-0xff189fff]
[    0.222974] pci 0000:00:07.1: PME# supported from D0 D3hot
[    0.223317] pci 0000:00:07.2: [8086:1194] type 00 class 0x088000
[    0.223385] pci 0000:00:07.2: reg 10: [mem 0xff18a000-0xff18afff]
[    0.223598] pci 0000:00:07.2: PME# supported from D0 D3hot
[    0.223954] pci 0000:00:08.0: [8086:1195] type 00 class 0x078000
[    0.224021] pci 0000:00:08.0: reg 10: [mem 0xff18b000-0xff18bfff]
[    0.224234] pci 0000:00:08.0: PME# supported from D0 D3hot
[    0.224560] pci 0000:00:08.1: [8086:1195] type 00 class 0x078000
[    0.224627] pci 0000:00:08.1: reg 10: [mem 0xff18c000-0xff18cfff]
[    0.224840] pci 0000:00:08.1: PME# supported from D0 D3hot
[    0.225179] pci 0000:00:08.2: [8086:1195] type 00 class 0x078000
[    0.225247] pci 0000:00:08.2: reg 10: [mem 0xff18d000-0xff18dfff]
[    0.225461] pci 0000:00:08.2: PME# supported from D0 D3hot
[    0.225787] pci 0000:00:08.3: [8086:1195] type 00 class 0x078000
[    0.225854] pci 0000:00:08.3: reg 10: [mem 0xff18e000-0xff18efff]
[    0.226066] pci 0000:00:08.3: PME# supported from D0 D3hot
[    0.226421] pci 0000:00:09.0: [8086:1196] type 00 class 0x078000
[    0.226488] pci 0000:00:09.0: reg 10: [mem 0xff18f000-0xff18ffff]
[    0.226701] pci 0000:00:09.0: PME# supported from D0 D3hot
[    0.227040] pci 0000:00:09.1: [8086:1196] type 00 class 0x078000
[    0.227107] pci 0000:00:09.1: reg 10: [mem 0xff190000-0xff190fff]
[    0.227320] pci 0000:00:09.1: PME# supported from D0 D3hot
[    0.227648] pci 0000:00:09.2: [8086:1196] type 00 class 0x078000
[    0.227716] pci 0000:00:09.2: reg 10: [mem 0xff191000-0xff191fff]
[    0.227928] pci 0000:00:09.2: PME# supported from D0 D3hot
[    0.228287] pci 0000:00:0a.0: [8086:1197] type 00 class 0x078000
[    0.228355] pci 0000:00:0a.0: reg 10: [mem 0xff3f8000-0xff3f8fff]
[    0.228569] pci 0000:00:0a.0: PME# supported from D0 D3hot
[    0.228911] pci 0000:00:0b.0: [8086:1198] type 00 class 0x108000
[    0.228978] pci 0000:00:0b.0: reg 10: [mem 0xf9038000-0xf903ffff]
[    0.229191] pci 0000:00:0b.0: PME# supported from D0 D3hot
[    0.229522] pci 0000:00:0c.0: [8086:1199] type 00 class 0x088000
[    0.229589] pci 0000:00:0c.0: reg 10: [mem 0xff008000-0xff008fff]
[    0.229632] pci 0000:00:0c.0: reg 14: [mem 0x000ddcc0-0x000ddccf]
[    0.229825] pci 0000:00:0c.0: PME# supported from D0 D3hot
[    0.230167] pci 0000:00:0d.0: [8086:119a] type 00 class 0x040100
[    0.230235] pci 0000:00:0d.0: reg 10: [mem 0x05e00000-0x05ffffff]
[    0.230277] pci 0000:00:0d.0: reg 14: [mem 0xff340000-0xff343fff]
[    0.230318] pci 0000:00:0d.0: reg 18: [mem 0xff344000-0xff344fff]
[    0.230358] pci 0000:00:0d.0: reg 1c: [mem 0xff2c0000-0xff2dffff]
[    0.230399] pci 0000:00:0d.0: reg 20: [mem 0xff300000-0xff33ffff]
[    0.230539] pci 0000:00:0d.0: PME# supported from D0 D3hot
[    0.230870] pci 0000:00:0e.0: [8086:119b] type 00 class 0x088000
[    0.230937] pci 0000:00:0e.0: reg 10: [mem 0xff298000-0xff29bfff]
[    0.230980] pci 0000:00:0e.0: reg 14: [mem 0xff2a2000-0xff2a2fff]
[    0.231173] pci 0000:00:0e.0: PME# supported from D0 D3hot
[    0.231525] pci 0000:00:11.0: [8086:119e] type 00 class 0x0c0320
[    0.231638] pci 0000:00:11.0: reg 10: [mem 0xf9100000-0xf911ffff]
[    0.231854] pci 0000:00:11.0: PME# supported from D0 D3hot
[    0.232201] pci 0000:00:12.0: [8086:119f] type 00 class 0x118000
[    0.232269] pci 0000:00:12.0: reg 10: [mem 0xf9009000-0xf9009fff]
[    0.232312] pci 0000:00:12.0: reg 14: [mem 0xf90a0000-0xf90affff]
[    0.232353] pci 0000:00:12.0: reg 18: [mem 0xfa000000-0xfaffffff]
[    0.232528] pci 0000:00:12.0: PME# supported from D0 D3hot
[    0.232916] pci 0000:00:13.0: [8086:11a0] type 00 class 0x0b4000
[    0.232984] pci 0000:00:13.0: reg 10: [mem 0xff009000-0xff009fff]
[    0.233196] pci 0000:00:13.0: PME# supported from D0 D3hot
[    0.233543] pci 0000:00:14.0: [8086:11a1] type 00 class 0x0b4000
[    0.233611] pci 0000:00:14.0: reg 10: [mem 0xff00b000-0xff00bfff]
[    0.233824] pci 0000:00:14.0: PME# supported from D0 D3hot
[    0.234171] pci 0000:00:15.0: [8086:11a2] type 00 class 0x088000
[    0.234238] pci 0000:00:15.0: reg 10: [mem 0xff192000-0xff192fff]
[    0.234451] pci 0000:00:15.0: PME# supported from D0 D3hot
[    0.234786] pci 0000:00:16.0: [8086:11a3] type 00 class 0x0b4000
[    0.234853] pci 0000:00:16.0: reg 10: [mem 0xff0d9000-0xff0d90ff]
[    0.235066] pci 0000:00:16.0: PME# supported from D0 D3hot
[    0.235411] pci 0000:00:16.1: [8086:11a4] type 00 class 0x0b4000
[    0.235479] pci 0000:00:16.1: reg 10: [mem 0x04819000-0x04898fff]
[    0.235522] pci 0000:00:16.1: reg 14: [mem 0x04919000-0x04920fff]
[    0.235715] pci 0000:00:16.1: PME# supported from D0 D3hot
[    0.236085] pci 0000:00:17.0: [8086:11a5] type 00 class 0x088000
[    0.236152] pci 0000:00:17.0: reg 10: [mem 0xff013000-0xff013fff]
[    0.236366] pci 0000:00:17.0: PME# supported from D0 D3hot
[    0.236703] pci 0000:00:18.0: [8086:11a6] type 00 class 0x038000
[    0.236955] pci 0000:00:18.0: PME# supported from D0 D3hot
[    0.237334] pci_bus 0000:00: busn_res: [bus 00-ff] end is updated to 00
[    0.237499] PCI: pci_cache_line_size set to 64 bytes
[    0.237764] e820: reserve RAM buffer [mem 0x00098000-0x0009ffff]
[    0.237784] e820: reserve RAM buffer [mem 0x3f500000-0x3fffffff]
[    0.238532] Bluetooth: Core ver 2.16
[    0.238615] NET: Registered protocol family 31
[    0.238631] Bluetooth: HCI device and connection manager initialized
[    0.238660] Bluetooth: HCI socket layer initialized
[    0.238685] Bluetooth: L2CAP socket layer initialized
[    0.238781] Bluetooth: SCO socket layer initialized
[    0.239472] cfg80211: Calling CRDA to update world regulatory domain
[    0.240720] intel_scu_flis platform device created
[    0.240797] hsu core clock 38 M
[    0.240969] intel_pmu_driver 0000:00:14.0: PMU DRIVER Probe called
[    0.242248] intel_pmu_driver 0000:00:14.0: after pmu initialization
[    0.242382] Switching to clocksource refined-jiffies
[    0.498421] intel_scu_flis rpmsg12: Probed flis rpmsg device
[    0.498447] intel_scu_flis rpmsg12: Allocating rpmsg_instance
[    0.498620] intel_scu_flis intel_scu_flis: scu flis probed
[    0.511248] pci_bus 0000:00: resource 4 [io  0x0000-0xffff]
[    0.511275] pci_bus 0000:00: resource 5 [mem 0x00000000-0xfffffffff]
[    0.511507] NET: Registered protocol family 2
[    0.512463] TCP established hash table entries: 8192 (order: 4, 65536 bytes)
[    0.512672] TCP bind hash table entries: 8192 (order: 5, 163840 bytes)
[    0.512966] TCP: Hash tables configured (established 8192 bind 8192)
[    0.513064] TCP: reno registered
[    0.513094] UDP hash table entries: 512 (order: 2, 24576 bytes)
[    0.513162] UDP-Lite hash table entries: 512 (order: 2, 24576 bytes)
[    0.513582] NET: Registered protocol family 1
[    0.514087] RPC: Registered named UNIX socket transport module.
[    0.514107] RPC: Registered udp transport module.
[    0.514121] RPC: Registered tcp transport module.
[    0.514133] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.516635] PCI: CLS 0 bytes, default 64
[    0.516725] intel_scu_pmic rpmsg8: Probed pmic rpmsg device
[    0.516747] intel_scu_pmic rpmsg8: Allocating rpmsg_instance
[    0.517395] intel_scu_watchdog_evo rpmsg13: Probed watchdog rpmsg device
[    0.517419] intel_scu_watchdog_evo rpmsg13: Allocating rpmsg_instance
[    0.518087] intel_scu_ipcutil rpmsg11: Probed ipcutil rpmsg device
[    0.518110] intel_scu_ipcutil rpmsg11: Allocating rpmsg_instance
[    0.518254] (oshob) base addr = 0xfffff000
[    0.518269] (oshob) identified platform = INTEL_MID_CPU_CHIP_TANGIER
[    0.518285] (oshob) oshob version = 1.4
[    0.518335] (latest extend oshob) osnib ptr = 0xfffff800
[    0.518350] Using latest extended oshob structure size = 1024 bytes
[    0.518364] OSNIB Intel size = 32 bytes OEMNIB size = 96 bytes
[    0.518377] (extend oshob) SCU buffer size is 16 bytes
[    0.518443] [BOOT] RESETSRC0=0x00 RESETSRC1=0x00 (PMIT interrupt tree)
[    0.518516] [BOOT] SCU_TR[0]=0x00020011
[    0.518530] [BOOT] SCU_TR[1]=0x00000220
[    0.518543] [BOOT] SCU_TR[2]=0x00000000
[    0.518556] [BOOT] SCU_TR[3]=0x00000000
[    0.518568] [BOOT] IA_TR=0x00000000 (oshob)
[    0.518904] [BOOT] RR=[fastboot] WD=0x00 ALARM=0x00 (osnib)
[    0.518919] [BOOT] WAKESRC=[no matching osip entry] (osnib)
[    0.518934] [BOOT] RESETSRC0=0x00 RESETSRC1=0x00 (osnib)
[    0.519003] OEMNIB interface registered to debugfs
[    0.519367] iio_basincove_gpadc rpmsg0: Probed bcove_gpadc rpmsg device
[    0.520076] bcove_adc bcove_adc: bcove adc probed
[    0.521062] platform rtc_cmos: registered platform RTC device (no PNP device found)
[    0.523151] cryptomgr_test (31) used greatest stack depth: 7532 bytes left
[    0.525660] vprog1: 1500 <--> 2800 mV at 2800 mV normal 
[    0.526406] vprog2: 1500 <--> 2850 mV at 2850 mV normal 
[    0.527153] vprog3: 1050 <--> 2800 mV at 1050 mV normal 
[    0.528469] audit: initializing netlink socket (disabled)
[    0.528542] type=2000 audit(946684808.450:1): initialized
[    0.677083] bounce pool size: 64 pages
[    0.694603] NFS: Registering the id_resolver key type
[    0.694695] Key type id_resolver registered
[    0.694712] Key type id_legacy registered
[    0.694743] Installing knfsd (copyright (C) 1996 okir@monad.swb.de).
[    0.695229] fuse init (API version 7.22)
[    0.696009] msgmni has been set to 1677
[    0.696567] SELinux:  Registering netfilter hooks
[    0.697754] cryptomgr_test (48) used greatest stack depth: 7368 bytes left
[    0.699720] Key type asymmetric registered
[    0.699741] Asymmetric key parser 'x509' registered
[    0.699851] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 249)
[    0.700112] io scheduler noop registered
[    0.700403] io scheduler cfq registered (default)
[    0.700420] list_sort_test: start testing list_sort()
[    0.703642] intel_idle: MWAIT substates: 0x33000020
[    0.703662] intel_idle: v0.4 model 0x4A
[    0.703677] intel_idle: lapic_timer_reliable_states 0xffffffff
[    0.703939] intel_mid_dma 0000:00:0e.0: setting latency timer to 64
[    0.704585] intel_mid_dma 0000:00:15.0: setting latency timer to 64
[    0.706269] HSU DMA 0000:00:05.0: FUNC: 0 driver: 5 addr:ff010400 len:400
[    0.706519] HSU serial 0000:00:04.0: FUNC: 0 driver: 0 addr:ff010000 len:80
[    0.706576] HSU serial 0000:00:04.1: FUNC: 1 driver: 0 addr:ff010080 len:80
[    0.706651] Found a Intel HSU
[    0.707485] 0000:00:04.1: ttyMFD0 at MMIO 0xff010080 (irq = 28) is a hsu_bt_port_p
[    0.708026] HSU serial 0000:00:04.2: FUNC: 2 driver: 0 addr:ff010100 len:80
[    0.708106] Found a Intel HSU
[    0.708930] 0000:00:04.2: ttyMFD1 at MMIO 0xff010100 (irq = 29) is a hsu_uart1_port_p
[    0.709452] HSU serial 0000:00:04.3: FUNC: 3 driver: 0 addr:ff010180 len:80
[    0.709532] Found a Intel HSU
[    0.710197] 0000:00:04.3: ttyMFD2 at MMIO 0xff010180 (irq = 54) is a hsu_uart2_port_p
[    0.714170] console [ttyMFD2] enabled
[    0.715304] Non-volatile memory driver v1.3
[    0.715985] Linux agpgart interface v0.103
[    0.716481] [drm] Initialized drm 1.1.0 20060810
[    0.730472] brd: module loaded
[    0.737927] loop: module loaded
[    0.740854] emmc_ipanic: init success
[    0.741636] tun: Universal TUN/TAP device driver, 1.6
[    0.741656] tun: (C) 1999-2004 Max Krasnyansky <maxk@qualcomm.com>
[    0.742072] usbcore: registered new interface driver asix
[    0.742153] usbcore: registered new interface driver cdc_subset
[    0.742282] usbcore: registered new interface driver cdc_ncm
[    0.742539] dwc3_otg 0000:00:11.0: setting latency timer to 64
[    0.744705] ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
[    0.745027] usbcore: registered new interface driver cdc_acm
[    0.745045] cdc_acm: USB Abstract Control Model driver for USB modems and ISDN adapters
[    0.745160] usbcore: registered new interface driver usb-storage
[    0.745339] usbcore: registered new interface driver usbserial
[    0.745410] usbcore: registered new interface driver pl2303
[    0.745477] usbserial: USB Serial support registered for pl2303
[    0.746394] rtc_cmos rtc_cmos: rtc core: registered rtc_cmos as rtc0
[    0.746557] rtc_cmos rtc_cmos: alarms up to one day, 114 bytes nvram
[    0.746611] i2c /dev entries driver
[    0.747590] pca953x 1-0020: failed reading register
[    0.752503] pca953x: probe of 1-0020 failed with error -121
[    0.752803] pca953x 1-0021: failed reading register
[    0.752892] pca953x: probe of 1-0021 failed with error -121
[    0.757900] pca953x 1-0022: failed reading register
[    0.757986] pca953x: probe of 1-0022 failed with error -121
[    0.763014] pca953x 1-0023: failed reading register
[    0.767826] pca953x: probe of 1-0023 failed with error -121
[    0.902722] coretemp: Enabled Aux0/Aux1 interrupts for coretemp
[    0.902853] coretemp: Enabled Aux0/Aux1 interrupts for coretemp
[    1.002377] MCU detected and ready to used!
[    1.002503] bcove_thrm rpmsg1: Probed mrfl_thermal rpmsg device
[    1.008539] thermal thermal_zone0: failed to read out thermal zone 0
[    1.009675] thermal thermal_zone2: failed to read out thermal zone 2
[    1.012347] Bluetooth: HCI UART driver ver 2.2
[    1.012369] Bluetooth: HCI H4 protocol initialized
[    1.012831] cpuidle: using governor ladder
[    1.013441] cpuidle: using governor menu
[    1.013510] sdhci: Secure Digital Host Controller Interface driver
[    1.013525] sdhci: Copyright(c) Pierre Ossman
[    1.013601] sdhci-pci 0000:00:01.0: SDHCI controller found [8086:1190] (rev 1)
[    1.013680] flis_addr mapped addr: f8496900
[    1.013803] sdhci-pci 0000:00:01.0: rte_addr mapped addr: f849a000
[    1.013863] sdhci-pci 0000:00:01.0: setting latency timer to 64
[    1.013893] mmc0: no vqmmc regulator found
[    1.106339] mmc0: BKOPS_EN bit is not set
[    1.415109] mmc0: new HS200 MMC card at address 0001
[    1.415899] mmcblk0: mmc0:0001 H4G1d 3.64 GiB 
[    1.416409] mmcblk0boot0: mmc0:0001 H4G1d partition 1 4.00 MiB
[    1.416876] mmcblk0boot1: mmc0:0001 H4G1d partition 2 4.00 MiB
[    1.417328] mmcblk0rpmb: mmc0:0001 H4G1d partition 3 4.00 MiB
[    1.423000]  mmcblk0: p1 p2 p3 p4 p5 p6 p7 p8 p9 p10
[    1.431286]  mmcblk0boot1: unknown partition table
[    1.434918]  mmcblk0boot0: unknown partition table
[    1.435317] mmc0: SDHCI controller on PCI [0000:00:01.0] using ADMA
[    1.454345] emmc_ipanic: panic partition found, label:panic, device:mmcblk0p6
[    1.514408] Switching to clocksource tsc
[    1.554043] emmc_ipanic: emmc_panic_notify_add: Data available in panic partition
[    1.554090] emmc_ipanic: emmc_panic_notify_add: proc entry created: emmc_ipanic_header
[    1.554112] emmc_ipanic: emmc_panic_notify_add: log file 0(1024, 44237)
[    1.554139] emmc_ipanic: emmc_panic_notify_add: proc entry created: emmc_ipanic_console
[    1.554156] emmc_ipanic: emmc_panic_notify_add: log file 1(4286578688, 0)
[    1.554170] emmc_ipanic: emmc_panic_notify_add: empty log file 1
[    1.554185] emmc_ipanic: emmc_panic_notify_add: log file 2(4286578688, 0)
[    1.554199] emmc_ipanic: emmc_panic_notify_add: empty log file 2
[    1.554288] sdhci-pci 0000:00:01.2: SDHCI controller found [8086:1190] (rev 1)
[    1.584957] sdhci-pci 0000:00:01.2: setting latency timer to 64
[    1.585001] mmc1: no vqmmc regulator found
[    1.585443] mmc1: SDHCI controller on PCI [0000:00:01.2] using ADMA
[    1.585632] sdhci-pci 0000:00:01.3: SDHCI controller found [8086:1190] (rev 1)
[    1.585748] vwlan gpio 96
[    1.586130] vwlan: 1800 mV 
[    1.586363] sdhci-pci 0000:00:01.3: setting latency timer to 64
[    1.586392] mmc2: no vqmmc regulator found
[    1.586838] mmc2: SDHCI controller on PCI [0000:00:01.3] using ADMA
[    1.595379] hidraw: raw HID events driver (C) Jiri Kosina
[    1.596029] usbcore: registered new interface driver usbhid
[    1.596048] usbhid: USB HID core driver
[    1.596129] intel_scu_fw_update rpmsg10: Probed fw_update rpmsg device
[    1.596149] intel_scu_fw_update rpmsg10: Allocating rpmsg_instance
[    1.600882] usbcore: registered new interface driver snd-usb-audio
[    1.601991] snd_soc_sst_platform: Enter:sst_soc_probe
[    1.960913] snd-soc-dummy snd-soc-dummy: ASoC: Failed to create platform debugfs directory
[    1.961162] merr_dpcm_dummy merr_dpcm_dummy.0:  snd-soc-dummy-dai <-> Headset-cpu-dai mapping ok
[    1.961298] merr_dpcm_dummy merr_dpcm_dummy.0:  snd-soc-dummy-dai <-> ssp2-codec mapping ok
[    1.961424] merr_dpcm_dummy merr_dpcm_dummy.0:  snd-soc-dummy-dai <-> snd-soc-dummy-dai mapping ok
[    1.963370] snd_merr_dpcm_probe successful
[    1.963456] snd_intel_sst: INFO: ******** SST DRIVER loading.. Ver: 3.0.8
[    1.963971] snd_intel_sst: Got drv data max stream 25
[    1.966759] snd_intel_sst: intel_sst_probe successfully done!
[    1.966824] snd_intel_sst: runtime_idle called
[    1.966844] snd_intel_sst: runtime_suspend called
[    1.967125] oprofile: using NMI interrupt.
[    1.967271] Netfilter messages via NETLINK v0.30.
[    1.967364] nf_conntrack version 0.5.0 (15352 buckets, 61408 max)
[    1.968236] NF_TPROXY: Transparent proxy support initialized, version 4.1.0
[    1.968254] NF_TPROXY: Copyright (c) 2006-2007 BalaBit IT Ltd.
[    1.968856] ip_tables: (C) 2000-2006 Netfilter Core Team
[    1.969156] TCP: cubic registered
[    1.969173] Initializing XFRM netlink socket
[    1.970315] NET: Registered protocol family 10
[    1.971652] ip6_tables: (C) 2000-2006 Netfilter Core Team
[    1.971987] sit: IPv6 over IPv4 tunneling driver
[    1.972918] NET: Registered protocol family 17
[    1.972980] NET: Registered protocol family 15
[    1.973128] Bridge firewalling registered
[    1.973489] Bluetooth: RFCOMM TTY layer initialized
[    1.973561] Bluetooth: RFCOMM socket layer initialized
[    1.973578] Bluetooth: RFCOMM ver 1.11
[    1.973594] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
[    1.973608] Bluetooth: BNEP filters: protocol multicast
[    1.973638] Bluetooth: BNEP socket layer initialized
[    1.973653] Bluetooth: HIDP (Human Interface Emulation) ver 1.2
[    1.973679] Bluetooth: HIDP socket layer initialized
[    1.973826] l2tp_core: L2TP core driver, V2.0
[    1.973912] Key type dns_resolver registered
[    1.975634] Using IPI No-Shortcut mode
[    1.975679] info[ 0]: name = power_btn, gpio = -1
[    1.975696] info[ 1]: name = SW1UI4, gpio = 61
[    1.976846] registered taskstats version 1
[    1.979192] intel_mid_ssp_spi_unified 0000:00:07.0: found PCI SSP controller (ID: 8086h:1194h cfg: 0dh)
[    1.980142] intel_mid_ssp_spi_unified 0000:00:07.0: register with SPI framework (bus spi3)
[    1.980305] intel_mid_ssp_spi_unified 0000:00:07.0: master is unqueued, this is deprecated
[    1.980335] intel_mid_ssp_spi_unified 0000:00:07.0: Unbalanced pm_runtime_enable!
[    1.984719] intel_mid_ssp_spi_unified 0000:00:07.1: found PCI SSP controller (ID: 8086h:1194h cfg: 15h)
[    1.985553] intel_mid_ssp_spi_unified 0000:00:07.1: register with SPI framework (bus spi5)
[    1.985728] intel_mid_ssp_spi_unified 0000:00:07.1: master is unqueued, this is deprecated
[    1.987532] intel_mid_ssp_spi_unified 0000:00:07.1: Unbalanced pm_runtime_enable!
[    1.994938] intel_mid_ssp_spi_unified 0000:00:07.2: found PCI SSP controller (ID: 8086h:1194h cfg: 19h)
[    1.995752] intel_mid_ssp_spi_unified 0000:00:07.2: register with SPI framework (bus spi6)
[    1.995916] intel_mid_ssp_spi_unified 0000:00:07.2: master is unqueued, this is deprecated
[    1.995944] intel_mid_ssp_spi_unified 0000:00:07.2: Unbalanced pm_runtime_enable!
[    2.004826] console [netcon0] enabled
[    2.004844] netconsole: network logging started
[    2.005376] input: gpio-keys as /devices/platform/gpio-keys/input/input0
[    2.005997] rtc_cmos rtc_cmos: setting system clock to 2000-01-01 00:00:10 UTC (946684810)
[    2.006075] pmic_ccsm rpmsg3: Probed pmic_ccsm rpmsg device
[    2.006299] pmic_ccsm pmic_ccsm: PMIC-ID: c9
[    2.006322] pmic_ccsm pmic_ccsm: Error reading battery profile from battid frmwrk
[    2.014961] pmic_ccsm pmic_ccsm: Battery Zone changed. Current zone is 5
[    2.017757] APIC ID: 0
[    2.017775] APIC ID: 2
[    2.017837] Num p-states 2
[    2.017855] State [0]: core_frequency[500] transition_latency[100] control[0x527]
[    2.017870] State [1]: core_frequency[500] transition_latency[100] control[0x527]
[    2.018029] Num p-states 2
[    2.018047] State [0]: core_frequency[500] transition_latency[100] control[0x527]
[    2.018062] State [1]: core_frequency[500] transition_latency[100] control[0x527]
[    2.018491] msic_power_btn rpmsg2: Probed mid_pb rpmsg device
[    2.018557] msic_power_btn mid_powerbtn: Probed mid powerbutton devivce
[    2.018910] input: mid_powerbtn as /devices/platform/mid_powerbtn/input/input1
[    2.020430] ALSA device list:
[    2.020449]   #0: Loopback 1
[    2.020463]   #1: dummy-audio
[    2.024518] pmic_ccsm pmic_ccsm: Battery Over heat exception
[    2.024586] pmic_ccsm pmic_ccsm: USB VBUS Detected. Notifying OTG driver
[    2.024608] pmic_ccsm pmic_ccsm: USB VBUS Detected. Notifying OTG driver
[    2.099972] EXT4-fs (mmcblk0p8): INFO: recovery required on readonly filesystem
[    2.099996] EXT4-fs (mmcblk0p8): write access will be enabled during recovery
[    2.130942] mmc2: queuing unknown CIS tuple 0x91 (3 bytes)
[    2.130981] mmc2: new ultra high speed DDR50 SDIO card at address 0001
[    2.169844] EXT4-fs (mmcblk0p8): recovery complete
[    2.172159] EXT4-fs (mmcblk0p8): mounted filesystem with ordered data mode. Opts: (null)
[    2.172251] VFS: Mounted root (ext4 filesystem) readonly on device 179:8.
[    2.173026] devtmpfs: mounted
[    2.173407] Freeing unused kernel memory: 572k freed
[    2.174181] Write protecting the kernel text: 7068k
[    2.175019] Write protecting the kernel read-only data: 2944k
[    2.175036] NX-protecting the kernel data: 5220k
[    2.402116] systemd[1]: systemd 213 running in system mode. (-PAM -AUDIT -SELINUX +IMA +SYSVINIT -LIBCRYPTSETUP -GCRYP)
[    2.403605] systemd[1]: Detected architecture 'x86'.
[    2.516796] systemd[1]: Set hostname to <edison>.
[    2.522979] systemd[1]: Hardware watchdog 'Intel_SCU IOH Watchdog', version 0
[    2.523065] systemd[1]: Set hardware watchdog to 1min 30s.
[    2.537229] systemd-system- (96) used greatest stack depth: 6364 bytes left
[    2.552346] systemd-fstab-generator[101]: Checking was requested for "rootfs", but it is not a device.
[    2.554774] systemd-fstab-g (101) used greatest stack depth: 6324 bytes left
[    2.558656] systemd-getty-g (99) used greatest stack depth: 5960 bytes left
[    2.753189] systemd[1]: Configuration file /lib/systemd/system/connman-init.service is marked executable. Please remov.
[    2.798354] systemd[1]: Expecting device dev-ttyMFD2.device...
[    2.844742] systemd[1]: Starting Forward Password Requests to Wall Directory Watch.
[    2.845378] systemd[1]: Started Forward Password Requests to Wall Directory Watch.
[    2.845505] systemd[1]: Expecting device sys-subsystem-net-devices-wlan0.device...
[    2.894630] systemd[1]: Starting Remote File Systems.
[    2.944603] systemd[1]: Reached target Remote File Systems.
[    2.944726] systemd[1]: Expecting device dev-disk-by\x2dpartlabel-factory.device...
[    2.994673] systemd[1]: Starting Dispatch Password Requests to Console Directory Watch.
[    2.995118] systemd[1]: Started Dispatch Password Requests to Console Directory Watch.
[    2.995231] systemd[1]: Starting Paths.
[    3.044592] systemd[1]: Reached target Paths.
[    3.044721] systemd[1]: Starting Swap.
[    3.094579] systemd[1]: Reached target Swap.
[    3.094700] systemd[1]: Starting boot.automount.
[    3.147586] systemd[1]: boot.automount: Directory /boot to mount over is not empty, mounting anyway.
[    3.194773] systemd[1]: Set up automount boot.automount.
[    3.194954] systemd[1]: Starting Root Slice.
[    3.314606] systemd[1]: Created slice Root Slice.
[    3.314756] systemd[1]: Starting User and Session Slice.
[    3.364570] systemd[1]: Created slice User and Session Slice.
[    3.364697] systemd[1]: Starting Delayed Shutdown Socket.
[    3.414537] systemd[1]: Listening on Delayed Shutdown Socket.
[    3.414658] systemd[1]: Starting /dev/initctl Compatibility Named Pipe.
[    3.464531] systemd[1]: Listening on /dev/initctl Compatibility Named Pipe.
[    3.464677] systemd[1]: Starting udev Control Socket.
[    3.514524] systemd[1]: Listening on udev Control Socket.
[    3.514669] systemd[1]: Starting udev Kernel Socket.
[    3.564519] systemd[1]: Listening on udev Kernel Socket.
[    3.564669] systemd[1]: Starting Journal Socket.
[    3.614515] systemd[1]: Listening on Journal Socket.
[    3.614703] systemd[1]: Starting System Slice.
[    3.664530] systemd[1]: Created slice System Slice.
[    3.664671] systemd[1]: Mounting Temporary Directory...
[    3.779865] systemd[1]: Starting system-serial\x2dgetty.slice.
[    3.844682] systemd[1]: Created slice system-serial\x2dgetty.slice.
[    3.844839] systemd[1]: Starting system-getty.slice.
[    3.894526] systemd[1]: Created slice system-getty.slice.
[    3.959855] systemd[1]: Starting Load Kernel Modules...
[    4.078448] systemd[1]: Starting Create list of required static device nodes for the current kernel...
[    4.111027] dhd_module_init in
[    4.111060] found wifi platform device wlan
[    4.111171] Power-up adapter 'DHD generic adapter'
[    4.115386] systemd[1]: Starting udev Coldplug all Devices...
[    4.158849] systemd[1]: Mounted Huge Pages File System.
[    4.159090] systemd[1]: Mounting Debug File System...
[    4.209874] systemd[1]: Mounting POSIX Message Queue File System...
[    4.329037] systemd[1]: Starting Apply Kernel Variables...
[    4.378359] systemd[1]: Starting Journal Service...
[    4.454455] systemd[1]: Started Journal Service.
[    4.499874] wifi_platform_set_power = 1
[    4.624182] EXT4-fs (mmcblk0p8): re-mounted. Opts: discard,barrier=1,data=ordered,noauto_da_alloc
[    4.704122] wifi_platform_bus_enumerate device present 1
[    4.729957] bcmsdh_sdmmc: bcmsdh_sdmmc_probe Enter
[    4.730248] bcmsdh_sdmmc: bcmsdh_sdmmc_probe Enter
[    4.730268] bus num (host idx)=2, slot num (rca)=1
[    4.730283] found adapter info 'DHD generic adapter'
[    4.740688] F1 signature OK, socitype:0x1 chip:0xa94c rev:0x2 pkg:0x0
[    4.742227] DHD: dongle ram size is set to 524288(orig 524288) at 0x0
[    4.744158] wifi_platform_get_mac_addr
[    4.744232] wifi_get_mac_addr_intel: unable to open /config/wifi/mac.txt
[    4.754501] wl_create_event_handler(): thread:wl_event_handler:7b started
[    4.754523] CFG80211-ERROR) wl_event_handler : tsk Enter, tsk = 0xf5401540
[    4.754985] dhd_attach(): thread:dhd_watchdog_thread:7c started
[    4.755163] dhd_attach(): thread:dhd_dpc:7d started
[    4.755195] dhd_deferred_work_init: work queue initialized 
[    4.764216] Dongle Host Driver, version 1.141.59 (r)
[    4.764216] Compiled in /data/jenkins_worker/workspace/edison-weekly/out/linux64/build/tmp/work/edison-poky-linux/bcm44
[    4.765312] Register interface [wlan0]  MAC: 00:00:00:00:00:00
[    4.765312] 
[    4.765339] dhd_prot_ioctl : bus is down. we have nothing to do
[    4.766004] bcmsdh_sdmmc: bcmsdh_sdmmc_probe Enter
[    4.766120] wifi_platform_set_power = 0
[    4.767207] wifi_platform_bus_enumerate device present 0
[    4.832347] g_multi gadget: using random host ethernet address
[    4.833412] usb0: MAC 02:00:86:d5:27:b6
[    4.833442] usb0: HOST MAC 0e:94:2e:5d:8b:9a
[    4.844113] g_multi gadget: Mass Storage Function, version: 2009/09/11
[    4.844139] g_multi gadget: Number of LUNs=1
[    4.844166]  lun0: LUN: file: /dev/mmcblk0p9
[    4.844367] g_multi gadget: Multifunction Composite Gadget
[    4.844386] g_multi gadget: g_multi ready
[    5.005331] systemd-modules (104) used greatest stack depth: 5468 bytes left
[    5.936352] systemd-udevd[141]: starting version 213
[    6.222891] g_multi gadget: high-speed config #1: Multifunction with RNDIS
[    6.366658] systemd-journald[114]: Received request to flush runtime journal from PID 1
[    7.930499] EXT4-fs (mmcblk0p5): mounted filesystem without journal. Opts: discard,barrier=1,data=ordered,noauto_da_alc
[   10.225662] 
[   10.225662] Dongle Host Driver, version 1.141.59 (r)
[   10.225662] Compiled in /data/jenkins_worker/workspace/edison-weekly/out/linux64/build/tmp/work/edison-poky-linux/bcm44
[   10.225697] wl_android_wifi_on in
[   10.225715] wifi_platform_set_power = 1
[   10.675603] EXT4-fs (mmcblk0p10): mounted filesystem with ordered data mode. Opts: discard,barrier=1,data=ordered,noauc
[   10.999546] F1 signature OK, socitype:0x1 chip:0xa94c rev:0x2 pkg:0x0
[   11.001124] DHD: dongle ram size is set to 524288(orig 524288) at 0x0
[   11.003580] dhdsdio_download_firmware: firmware path=/etc/firmware/fw_bcmdhd.bin, nvram path=/etc/firmware/bcmdhd.cal
[   11.143719] sdioh_request_buffer: [1] doing memory copy buf=f5e9e000, len=18
[   11.232086] dhdsdio_write_vars: Download, Upload and compare of NVRAM succeeded.
[   11.391368] dhd_bus_init: enable 0x06, ready 0x06 (waited 0us)
[   11.394820] wifi_platform_get_mac_addr
[   11.394863] wifi_get_mac_addr_intel: unable to open /config/wifi/mac.txt
[   11.408369] Firmware up: op_mode=0x0015, MAC=78:4b:87:a7:e0:19
[   11.427094] Firmware version = wl0: Jan 30 2015 19:22:32 version 6.20.190.3 (r530911) FWID 01-5b07cccc
[   11.428142] dhd_preinit_ioctls wl ampdu_hostreorder failed -23
[   11.523861] CFG80211-ERROR) wl_update_wiphybands : bw_cap failed, -23
[   11.674729] CFGP2P-ERROR) wl_cfgp2p_add_p2p_disc_if : P2P interface registered
[   11.715488] WLC_E_IF: NO_IF set, event Ignored
[   12.317505] FAT-fs (mmcblk0p7): Volume was not properly unmounted. Some data may be corrupt. Please run fsck.
[   12.423519] snd_intel_sst: runtime_resume called
[   12.454497] snd_intel_sst: FW Version 01.09.00.02
[   12.454522] snd_intel_sst: Build date Jan 14 2014 Time 20:08:46
[   12.454628] snd_intel_sst: Alloc for str 14 pipe 0xe
[   12.778658] snd_intel_sst: Free for str 14 pipe 0xe
[   12.780318] snd_intel_sst: runtime_idle called
[   12.890778] snd_intel_sst: Alloc for str 14 pipe 0xe
[   12.992234] snd_intel_sst: Free for str 14 pipe 0xe
[   12.995377] snd_intel_sst: runtime_idle called
[   13.046553] snd_intel_sst: Alloc for str 1 pipe 0x90
[   13.201102] snd_intel_sst: Alloc for str 14 pipe 0xe
[   13.212069] snd_intel_sst: Free for str 14 pipe 0xe
[   13.219775] snd_intel_sst: Alloc for str 14 pipe 0xe
[   13.226118] snd_intel_sst: Free for str 14 pipe 0xe
[   13.228835] snd_intel_sst: Free for str 1 pipe 0x90
[   13.231433] snd_intel_sst: runtime_idle called
[   13.264806] snd_intel_sst: Alloc for str 1 pipe 0x90
[   13.354872] snd_intel_sst: Start for str 1 pipe 0x90
[   13.363932] snd_intel_sst: Alloc for str 14 pipe 0xe
[   13.445406] snd_intel_sst: Start for str 14 pipe 0xe
[   16.219062] CFG80211-ERROR) wl_cfg80211_connect : Connectting withf8:01:13:a8:2b:40 channel (1) ssid "INFINITUMfjph", )
[   16.219062] 
[   16.483675] wl_bss_connect_done succeeded with f8:01:13:a8:2b:40
[   16.490687] wl_bss_connect_done succeeded with f8:01:13:a8:2b:40
[   17.517489] ip (333) used greatest stack depth: 5208 bytes left
[   18.763162] snd_intel_sst: Stop for str 14 pipe 0xe
[   18.763942] snd_intel_sst: Free for str 14 pipe 0xe
[   18.769299] snd_intel_sst: Stop for str 1 pipe 0x90
[   18.769717] snd_intel_sst: Free for str 1 pipe 0x90
[   18.772246] snd_intel_sst: runtime_idle called
[   20.772314] snd_intel_sst: runtime_suspend called
[  238.901921] CFG80211-ERROR) wl_cfg80211_disconnect : Reason 3
[  238.905991] CFG80211-ERROR) wl_is_linkdown : Link down Reason : WLC_E_LINK
[  238.906032] link down if wlan0 may call cfg80211_disconnected. event : 16, reason=2 from f8:01:13:a8:2b:40
[  238.908662] CFG80211-ERROR) wl_is_linkdown : Link down Reason : WLC_E_DEAUTH
[  238.908691] CFG80211-ERROR) wl_is_linkdown : Link down Reason : WLC_E_DEAUTH
[  238.908711] CFG80211-ERROR) wl_is_linkdown : Link down Reason : WLC_E_DEAUTH
[  238.918812] cfg80211: Calling CRDA for country: MX
[  238.932636] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready
[  243.352020] CFG80211-ERROR) wl_cfg80211_connect : Connectting withf8:01:13:a8:2b:40 channel (1) ssid "INFINITUMfjph", )
[  243.352020] 
[  243.466639] wl_bss_connect_done succeeded with f8:01:13:a8:2b:40
[  243.473988] wl_bss_connect_done succeeded with f8:01:13:a8:2b:40
[  246.103863] ip (397) used greatest stack depth: 5092 bytes left
[  247.843088] systemd-fstab-generator[428]: Checking was requested for "rootfs", but it is not a device.
[  248.303659] systemd-fstab-generator[437]: Checking was requested for "rootfs", but it is not a device.
[  248.776434] systemd-fstab-generator[446]: Checking was requested for "rootfs", but it is not a device.

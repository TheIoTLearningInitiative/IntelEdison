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
    arch/x86/include/asm/intel_mid_vrtc.h
    arch/x86/include/asm/intel_mip.h

### MIP

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
    
    OSHOB-OS Handoff Buffer
    OSNIB interface
    scu_ipc_pmdb_buffer

### Virtual Real Time Clock (VRTC)

> VRTC is emulated by system controller firmware, the real HW RTC is located in the PMIC device. SCU FW shadows PMIC RTC in a memory mapped IO space that is visible to the host IA processor. This driver is based on RTC CMOS driver.

> Moorestown platform doesn't have a m146818 RTC device like traditional x86 PC, but a firmware emulated virtual RTC device(vrtc), which provides some basic RTC functions like get/set time. vrtc serves as the only wall clock device on Moorestown platform.

> Currently, vrtc init func will be called as arch_initcall() before xtime's init. Also move the sfi vrtc table parsing from mrst.c to vrtc.c

There will be another general vrtc driver for rtc subsystem

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

### GPIO
arch/x86/include/asm/gpio.h

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

Owner: Abraham

> Intel Silvermont (Atom)

> Intel MID is Intel's Low Power Intel Architecture (LPIA) based Mobile Internet Device(MID) platform. Unlike standard x86 PCs, Intel MID does not have many legacy devices nor standard legacy replacement devices/features. e.g. It does not contain i8259, i8254, HPET, legacy BIOS, most of the io ports.

    x86 Intel MID Platform
    bcm43340
    Medfield MID Platform
    Intel MID Platform
    
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

bcm43340
https://www.broadcom.com/products/wireless-connectivity/bluetooth/bcm43341

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
 drivers/pci/pci-atom_soc.c                         |   78 +
 drivers/pci/pci.c                                  |    5 +-
 drivers/pci/quirks.c                               |    6 +-
 drivers/platform/x86/Kconfig                       |   40 +
 drivers/platform/x86/Makefile                      |    6 +-
 drivers/platform/x86/intel_mid_powerbtn.c          |  252 +-
 drivers/platform/x86/intel_mid_thermal.c           |  574 --
 drivers/platform/x86/intel_pmic_gpio.c             |    2 +-
 drivers/platform/x86/intel_psh_ipc.c               |  637 +++
 drivers/platform/x86/intel_scu_flis.c              |  747 +++
 drivers/platform/x86/intel_scu_fw_update.c         | 1087 ++++
 drivers/platform/x86/intel_scu_ipc.c               |  636 +--
 drivers/platform/x86/intel_scu_ipcutil.c           | 2587 ++++++++-
 drivers/platform/x86/intel_scu_mip.c               |  776 +++
 drivers/platform/x86/intel_scu_pmic.c              |  477 ++

arch/x86/configs/i386_edison_defconfig
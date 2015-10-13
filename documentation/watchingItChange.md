# Watching it change

To see the status of our exported pins in the Edison, type this your terminal:

```
root@edison:/# watch -n 1 cat /sys/kernel/debug/gpio
```
Basically, it will output the configured GPIO's to console every second:

```
Every 1s: cat /sys/kernel/debug/gpio                        2015-10-13 21:02:27

GPIOs 0-191, pci/0000:00:0c.0, 0000:00:0c.0:
 gpio-61  (SW1UI4              ) in  hi
 gpio-64  (bcm43xx_irq         ) in  hi
 gpio-71  (bcm_bt_lpm          ) out lo
 gpio-77  (sd_cd               ) in  hi
 gpio-96  (vwlan               ) out hi
 gpio-111 (Arduino Shield SS   ) out hi
 gpio-124 (hsu                 ) in  hi
 gpio-125 (hsu                 ) in  hi
 gpio-126 (hsu                 ) in  hi
 gpio-127 (hsu                 ) in  hi
 gpio-128 (hsu                 ) in  hi
 gpio-129 (hsu                 ) in  hi
 gpio-130 (hsu                 ) in  hi
 gpio-131 (hsu                 ) in  hi
 gpio-132 (hsu                 ) in  lo
 gpio-133 (hsu                 ) out lo
 gpio-134 (hsu                 ) in  hi
 gpio-184 (bcm_bt_lpm          ) out lo
 gpio-185 (bcm_bt_lpm          ) in  lo

GPIOs 200-215, i2c/1-0020, pcal9555a, can sleep:
 gpio-207 (sysfs               ) in  hi
 gpio-215 (sysfs               ) out lo

GPIOs 216-231, i2c/1-0021, pcal9555a, can sleep:

GPIOs 232-247, i2c/1-0022, pcal9555a, can sleep:

GPIOs 248-263, i2c/1-0023, pcal9555a, can sleep:

```





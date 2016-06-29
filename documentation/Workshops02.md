# The Grove Starter Kit Plus Workshop

Time

- 90 minutes

Requirements

- Laptop
- Internet Connection
- Intel Edison
- [Grove Indoor Environment Kit for Intel® Edison](https://www.seeedstudio.com/item_detail.html?p_id=2427)
  - [Grove – Button](http://www.seeedstudio.com/wiki/Grove_-_Button)
    ![](http://www.seeedstudio.com/wiki/images/thumb/c/ca/Button.jpg/300px-Button.jpg)
  - [Grove - Touch Sensor](http://www.seeedstudio.com/wiki/Grove_-_Touch_Sensor)
  - ![](http://www.seeedstudio.com/wiki/images/thumb/a/a2/Twig-Touch.jpg/300px-Twig-Touch.jpg)
  - [Grove - Buzzer](http://www.seeedstudio.com/wiki/Grove_-_Buzzer)
    ![](http://www.seeedstudio.com/wiki/images/thumb/e/ed/Buzzer1.jpg/400px-Buzzer1.jpg) 
  - [Grove - Rotary Angle Sensor(P)](http://www.seeedstudio.com/wiki/Grove_-_Rotary_Angle_Sensor)
    ![](http://www.seeedstudio.com/wiki/images/thumb/a/af/Grove_-_Rotary_Angle_Sensor_%28P%29.jpg/400px-Grove_-_Rotary_Angle_Sensor_%28P%29.jpg)
  - [Grove - Light Sensor](http://www.seeedstudio.com/wiki/Grove_-_Light_Sensor)
    ![](http://www.seeedstudio.com/wiki/images/thumb/1/1c/Twig-Light.jpg/500px-Twig-Light.jpg)
  - [Grove - Temperature Sensor](http://www.seeedstudio.com/wiki/Grove_-_Temperature_Sensor)
    ![](http://www.seeedstudio.com/wiki/images/thumb/b/b0/Temperature1.jpg/400px-Temperature1.jpg)
- [Grove - LCD RGB Backlight](http://www.seeedstudio.com/wiki/Grove_-_LCD_RGB_Backlight)
    ![](http://www.seeedstudio.com/wiki/images/thumb/0/03/Serial_LEC_RGB_Backlight_Lcd.jpg/500px-Serial_LEC_RGB_Backlight_Lcd.jpg)

# Agenda

- [Grove – Button](http://www.seeedstudio.com/wiki/Grove_-_Button)
- [Grove - Touch Sensor](http://www.seeedstudio.com/wiki/Grove_-_Touch_Sensor)
- [Grove - Buzzer](http://www.seeedstudio.com/wiki/Grove_-_Buzzer)
- [Grove - Rotary Angle Sensor(P)](http://www.seeedstudio.com/wiki/Grove_-_Rotary_Angle_Sensor)
- [Grove - Light Sensor](http://www.seeedstudio.com/wiki/Grove_-_Light_Sensor)
- [Grove - Temperature Sensor](http://www.seeedstudio.com/wiki/Grove_-_Temperature_Sensor)
- [Grove - LCD RGB Backlight](http://www.seeedstudio.com/wiki/Grove_-_LCD_RGB_Backlight)

# Grove Starter Kit Plus

## Grove – Button

> Author: Sarah Knepper <sarah.knepper@intel.com>
> Copyright (c) 2014 Intel Corporation.

```sh
root@edison:~# vi button.py
```

```python
import time
import pyupm_grove as grove

# Create the button object using GPIO pin 2
button = grove.GroveButton(2)

# Read the input and print, waiting one second between readings
while 1:
    print button.name(), ' value is ', button.value()
    time.sleep(1)

# Delete the button object
del button
```

```sh
root@edison:~# python button.py
```

## Grove - Touch Sensor

> Author: Sarah Knepper <sarah.knepper@intel.com>
> Copyright (c) 2014 Intel Corporation.

```sh
root@edison:~# vi button.py
```

```python
import time
import pyupm_grove as grove

# Create the button object using GPIO pin 3
touch = grove.GroveButton(3)

# Read the input and print, waiting one second between readings
while 1:
    print touch.name(), ' value is ', touch.value()
    time.sleep(1)

# Delete the touch object
del touch
```

```sh
root@edison:~# python button.py
```

## Grove - Buzzer

> Author: 
> 

```sh
root@edison:~# vi .py
```

```python

```

```sh
root@edison:~# python .py
```

## Grove - Rotary Angle Sensor(P)

> Author: 
> 

```sh
root@edison:~# vi .py
```

```python

```

```sh
root@edison:~# python .py
```

## Grove - Light Sensor

> Author: 
> 

```sh
root@edison:~# vi .py
```

```python

```

```sh
root@edison:~# python .py
```

## Grove - Temperature Sensor

> Author: 
> 

```sh
root@edison:~# vi .py
```

```python

```

```sh
root@edison:~# python .py
```

## Grove - LCD RGB Backlight

> Author: 
> 

```sh
root@edison:~# vi .py
```

```python

```

```sh
root@edison:~# python .py
```

## Challenge

Create an application using all components...

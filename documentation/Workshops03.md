# The Twitter Project

Time

- 90 minutes

Requirements

- Laptop
- Internet Connection
- Intel Edison
- [Grove Indoor Environment Kit for Intel® Edison](https://www.seeedstudio.com/item_detail.html?p_id=2427)
  - [Grove - Temperature Sensor](http://www.seeedstudio.com/wiki/Grove_-_Temperature_Sensor)
   ![](http://www.seeedstudio.com/wiki/images/thumb/b/b0/Temperature1.jpg/400px-Temperature1.jpg)
  - [Grove - LCD RGB Backlight](http://www.seeedstudio.com/wiki/Grove_-_LCD_RGB_Backlight)
    ![](http://www.seeedstudio.com/wiki/images/thumb/0/03/Serial_LEC_RGB_Backlight_Lcd.jpg/500px-Serial_LEC_RGB_Backlight_Lcd.jpg)

# Agenda

- Base Project
  - Cloning 
  - Dependencies Setup
  - Project Execution
- Twitter
- Python Twitter Libraries
  - 
- Challenge

# Twitter


![](https://pbs.twimg.com/profile_images/666407537084796928/YBGgi9BO.png)¿

> Twitter is an online social networking service that enables users to send and read short 140-character messages called "tweets". Registered users can read and post tweets, but those who are unregistered can only read them. [Wikipedia](https://en.wikipedia.org/wiki/Twitter)
 
[Twitter Homepage](https://twitter.com/)

# Grove Starter Kit Plus

## Grove – Button

> Author: Sarah Knepper <sarah.knepper@intel.com>
> Copyright (c) 2014 Intel Corporation.

- [UPM Python Grove Button](https://github.com/intel-iot-devkit/upm/blob/master/examples/python/grovebutton.py)

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


## Grove - LCD RGB Backlight

> Author: Brendan Le Foll <brendan.le.foll@intel.com>
> Copyright (c) 2014 Intel Corporation.

- [UPM Python Grove LCD RGB Backlight](https://github.com/intel-iot-devkit/upm/blob/master/examples/python/jhd1313m1-lcd.py)

```sh
root@edison:~# vi lcd.py
```

```python
import pyupm_i2clcd as lcd

# Initialize Jhd1313m1 at 0x3E (LCD_ADDRESS) and 0x62 (RGB_ADDRESS) 
myLcd = lcd.Jhd1313m1(0, 0x3E, 0x62)

myLcd.setCursor(0,0)
# RGB Blue
#myLcd.setColor(53, 39, 249)

# RGB Red
myLcd.setColor(255, 0, 0)

while True:
    myLcd.write('Hello World')
    myLcd.setCursor(1,2)
    myLcd.write('Hello World')
```

```sh
root@edison:~# python lcd.py
```

# Twitter

## Cloning

```sh
root@edison:~# cd
root@edison:~# mkdir myproject
root@edison:~# cd myproject/
root@edison:~/myproject# git clone https://github.com/xe1gyq/core.git
Cloning into 'core'...
remote: Counting objects: 1109, done.
remote: Compressing objects: 100% (171/171), done.
remote: Total 1109 (delta 93), reused 0 (delta 0), pack-reused 924
Receiving objects: 100% (1109/1109), 217.79 KiB | 0 bytes/s, done.
Resolving deltas: 100% (605/605), done.
Checking connectivity... done.
root@edison:~/myproject# 
```

## Dependencies Setup

```sh
root@edison:~/myproject# pip install twython
root@edison:~/myproject# 
```

## Credentials Setup

```sh
root@edison:~/myproject# nano core/configuration/credentials.config
```

```sh
# Twitter
#
# Go to dev.twitter.com and sign up
# Go to Tools -> Manage Your Apps (Application Management)
# Create a New Application and go to "Keys and Access Tokens" tab
# Generate and get under Application Settings section:
#  Consumer Key (API Key), Consumer Secret (API Secret)
# Generate and get under Your Access Token section
#  Access Token and Access Token Secret
# Give Access Level "Read and Write"
[twitter]
consumer_key = 
consumer_secret = 
access_token = 
access_token_secret = 
```

## Your Code Twitter

```sh
root@edison:~/myproject# nano twittersample.py
```

```Python
    from core.xtweet import xTwitter
    
    itweet('#TheIoTLearningInitiative Testing Time', None)
```

```sh
root@edison:~# python twittersample.py
```

Look at your Twitter account...

## Challenge

Create an application using Twitter, Button and LCD... Button can be used to push a tweet (Core library usage will be enough) and LCD can be used to display latest tweet (direct usage of Twython API is required) 

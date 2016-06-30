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

# Base Project

# Cloning

```sh
```

## Dependencies Setup

```sh
```

## Project Execution

```sh
```

# Twitter


![](https://pbs.twimg.com/profile_images/666407537084796928/YBGgi9BO.png)¿

> 

# Python Telegram Bot Library

> Not just a Python Wrapper around the Telegram Bot API [Homepage](https://python-telegram-bot.org/) [Github](https://github.com/python-telegram-bot)

```sh
root@edison:~# pip install requests --upgrade
root@edison:~# pip install future --upgrade
root@edison:~# pip install python-telegram-bot --upgrade
```

```sh
root@edison:~# cd
root@edison:~# git clone https://github.com/python-telegram-bot/python-telegram-bot.git
Cloning into 'python-telegram-bot'...
remote: Counting objects: 5289, done.
remote: Total 5289 (delta 0), reused 0 (delta 0), pack-reused 5289
Receiving objects: 100% (5289/5289), 1.52 MiB | 772.00 KiB/s, done.
Resolving deltas: 100% (3876/3876), done.
Checking connectivity... done.
root@edison:~# cd python-telegram-bot
root@edison:~/python-telegram-bot# python setup.py install
...
...
root@edison:~# cd
```

## Telegram Bot @ Intel Edison

```sh
root@edison:~# vi telegrambot.py
```

```python
#!/usr/bin/python

import time

import pyupm_grove as grove
import pyupm_i2clcd as lcd

from telegram.ext import Updater, CommandHandler, MessageHandler, Filters

light = grove.GroveLight(1)
temperature = grove.GroveTemp(0)
display = lcd.Jhd1313m1(0, 0x3E, 0x62)

def functionLight(bot, update):
    luxes = light.value()
    bot.sendMessage(update.message.chat_id, text='Light ' + str(luxes))

def functionTemperature(bot, update):
    degrees = temperature.value()
    bot.sendMessage(update.message.chat_id, text='Temperature ' + str(degrees))

def functionEcho(bot, update):
    bot.sendMessage(update.message.chat_id, text=update.message.text)

if __name__ == '__main__':

    updater = Updater("219701132:AAEBn3_9ZBN-Lk8l8kRnkLKegmjA-S5iPaQ")
    dp = updater.dispatcher

    dp.add_handler(CommandHandler("light", functionLight))
    dp.add_handler(CommandHandler("temperature", functionTemperature))
    dp.add_handler(MessageHandler([Filters.text], functionEcho))

    updater.start_polling()

    while True:

        degrees = temperature.value()
        luxes = light.value()

        display.setColor(255, 0, 0)

        display.setCursor(0,0)
        display.write('Light ' + str(luxes))

        display.setCursor(1,0)
        display.write('Temperature ' + str(degrees))

        time.sleep(1)

    updater.idle()
    del temperatura
```

```sh
root@edison:~# python telegrambot.py
```

- Interact with your Bot using the Web Telegram Org Application

## Challenge

Integrate Telegram Bot code into "The IoT Learning Initiative" code

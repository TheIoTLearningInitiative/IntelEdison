# Intel Edison 2 Hours Workshop

Requirements

- Intel Edison
- [Grove Indoor Environment Kit for Intel® Edison](https://www.seeedstudio.com/item_detail.html?p_id=2427)
- Internet Connection
- Laptop

# Flashing

## Installer

- Download the specific installer from [Intel Edison Installers](https://software.intel.com/en-us/iot/hardware/edison/downloads)
  - Double click
    - Select "USB drivers installed"
    - Finish
  - Firmware version installed: not detected. Latest available: 201606061707
    - Flash Firmware
      - C:\Intel\Edison\Image\edison-image-20160606
      - Use existing image located at 

## Serial Clients

- Putty @ Windows
  - Session Connection Type: Serial
  - Session Serial Linea: COMx
  - Session Speed: 115200
  - Connection Serial Flow Control: None

- Screen || Minicom @ Linux
  - Session Connection Type: Serial
  - Session Serial Linea: /dev/tttyUSBx
  - Session Speed: 115200
  - Connection Serial Flow Control: None

# Booting

```sh
Poky (Yocto Project Reference Distro) 1.7.3 edison ttyMFD2                      
                                                                                
edison login: root                                                              
Last login: Mon Jun  6 21:33:16 UTC 2016 on ttyMFD2
```

Check your kernel version

```sh
root@edison:~# uname -r                                                         
3.10.98-poky-edison+                                                            
root@edison:~# 

```

Configure your Edison WiFi network

```sh
root@edison:~# configure_edison --wifi
Configure Edison: WiFi Connection

Scanning: 1 seconds left  

0 :     Rescan for networks
1 :     Exit WiFi Setup
2 :     Manually input a hidden SSID
3 :     CACUNAT
4 :     INFINITUMf89t
5 :     INFINITUM09E845
6 :     17057Abril
7 :     INFINITUMndjj
8 :     INFINITUMfjph


Enter 0 to rescan for networks.
Enter 1 to exit.
Enter 2 to input a hidden network SSID.
Enter a number between 3 to 8 to choose one of the listed network SSIDs: 8
Is INFINITUMfjph correct? [Y or N]: Y
Password must be between 8 and 63 characters.
What is the network password?: **********
Initiating connection to INFINITUMfjph. Please wait...                          
Attempting to enable network access, please check 'wpa_cli status' after a minu.
Done. Please connect your laptop or PC to the same network as this device and g.
Warning: SSH is not yet enabled on the wireless interface. To enable SSH access.
root@edison:~# 
```

```sh
root@edison:~# ping -c 2 8.8.8.8                                                
PING 8.8.8.8 (8.8.8.8): 56 data bytes                                           
64 bytes from 8.8.8.8: seq=0 ttl=59 time=151.659 ms                             
64 bytes from 8.8.8.8: seq=1 ttl=59 time=43.713 ms                              
                                                                                
--- 8.8.8.8 ping statistics ---                                                 
2 packets transmitted, 2 packets received, 0% packet loss                       
round-trip min/avg/max = 43.713/97.686/151.659 ms                               
root@edison:~# 
```

# Project Cloning

```sh
root@edison:~# git clone https://github.com/xe1gyq/TheIoTLearningInitiative.git
root@edison:~# cd TheIoTLearningInitiative/InternetOfThings101
root@edison:~/TheIoTLearningInitiative/InternetOfThings101#
root@edison:~/TheIoTLearningInitiative/InternetOfThings101# pip install -r requirements.pip
root@edison:~/TheIoTLearningInitiative/InternetOfThings101# sh requirements.manual
root@edison:~/TheIoTLearningInitiative/InternetOfThings101# 
```

```sh
root@edison:~/TheIoTLearningInitiative/InternetOfThings101# python main.py 
Hello Internet of Things 101
Data Sensor: 11513 
Data Sensor Mqtt Published!
API Weather: Guadalajara, JO, Mexico, Temperature 18 C, Atmospheric Pressure 842 mbar 
Data Sensor Mqtt Published!
Data Sensor Mqtt Published!
Data Sensor Mqtt Published!
Data Sensor Mqtt Published!
Data Sensor Mqtt Published!
Hello Internet of Things 101
Data Sensor: 11617 
API Weather: Guadalajara, JO, Mexico, Temperature 18 C, Atmospheric Pressure 842 mbar 
Data Sensor Mqtt Published!
^Z
[6]+  Stopped(SIGTSTP)        python main.py
root@edison:~/TheIoTLearningInitiative/InternetOfThings101# 
```


# Telegram Bots


![Telegram](https://telegram.org/img/t_logo.png)


> Bots are simply Telegram accounts operated by software – not people – and they'll often have AI features. They can do anything – teach, play, search, broadcast, remind, connect, integrate with other services, or even pass commands to the Internet of Things [Bot Revolution](https://telegram.org/blog/bot-revolution)

## Bot Code Examples

> Many members of our community are building bots and publishing the source code. We collect these examples here. Ping us on BotSupport if you've built a bot and would like to share its code with others [Bot Code Examples](https://core.telegram.org/bots/samples)

## BotFather

```sh
BotFather:
They call me the Botfather, I can help you create and set up Telegram bots. Please read this manual before we begin:
https://core.telegram.org/bots

You can control me by sending these commands:

/newbot - create a new bot
/token - generate authorization token
/revoke - revoke bot access token
/setname - change a bot's name
/setdescription - change bot description
/setabouttext - change bot about info
/setuserpic - change bot profile photo
/setinline - change inline settings
/setinlinegeo - toggle inline location requests
/setinlinefeedback - change inline feedback settings
/setcommands - change bot commands list
/setjoingroups - can your bot be added to groups?
/setprivacy - what messages does your bot see in groups?
/deletebot - delete a bot
/cancel - cancel the current operation
```

## Bot Creation

```sh
Abraham:
/newbot

[7:31:40 PM] BotFather:
Alright, a new bot. How are we going to call it? Please choose a name for your bot.

[7:31:57 PM] Abraham:
Xe1GyqExample

[7:31:58 PM] BotFather:
Good. Now let's choose a username for your bot. It must end in `bot`. Like this, for example: TetrisBot or tetris_bot.

[7:32:06 PM] Abraham:
Xe1GyqExampleBot

[7:32:08 PM] BotFather:
Done! Congratulations on your new bot. You will find it at telegram.me/Xe1GyqExampleBot. You can now add a description, about section and profile picture for your bot, see /help for a list of commands. By the way, when you've finished creating your cool bot, ping our Bot Support if you want a better username for it. Just make sure the bot is fully operational before you do this.

Use this token to access the HTTP API:
231219005:BBFq9seF0LfVuUvjifc8cBYfCngGcbcGdYs

For a description of the Bot API, see this page: https://core.telegram.org/bots/api
CANCELFORWARD 1 DELETE 1 REPLY
```

## Python Telegram Bot Library Installation

> Not just a Python Wrapper around the Telegram Bot API [Homepage](https://python-telegram-bot.org/) [Github](https://github.com/python-telegram-bot)

![Python Telegram Bot](https://raw.githubusercontent.com/python-telegram-bot/logos/master/logo/png/ptb-logo_240.png)


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

# Bot Example

```sh
root@edison:~# vi mybot.py
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
root@edison:~# python mybot.py
```

# Challenge

Integrate Telegram Bot code into "The IoT Learning Initiative" code
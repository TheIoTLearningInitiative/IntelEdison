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

# Base Project

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

## Core Twitter Execution

Modify


```sh
    $ python core/xtwitter.py
```

## Your Code Twitter

```sh
root@edison:~# vi twittersample.py
```

```Python
    from core.xtweet import xTwitter
    
    itweet('#TheIoTLearningInitiative Testing Time', None)
```

```sh
root@edison:~# python twitter.py
```

## Challenge



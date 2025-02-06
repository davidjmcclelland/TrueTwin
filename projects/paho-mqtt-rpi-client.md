---
icon: raspberry-pi
---

# Paho MQTT RPi Client

<figure><img src="../.gitbook/assets/PiCloudTwin2.webp" alt=""><figcaption><p>A Raspberry Pi Cloud Connection Concept</p></figcaption></figure>

#### Why Use Paho?

Paho is an MQTT client implementation maintained by the Apache Foundation. There are libraries available to ease integrating it into several languages. These aspects make it a good choice for a project where multiple popular languages will be used. There are differences between the languages but a lot of similarity in the implementations.

The Paho library will be useful to connect the Raspberry Pi GPIO interface with an MQTT server because it is available as a [plugin for Python](https://pypi.org/project/paho-mqtt/). I built and ran it on a PC to get the server connection details ironed out before using it with the GPIO handler on the Pi.

#### Quick Start

HiveMQ provides a number of different sample implementations including one in Python. I chose to use it as my starting point to create my message handler on my Pi, and named it lightStatus.py. First I had to update its configuration to connect and communicate with the HiveMQ free server from my PC. I did this running the code in my IDE terminal. I started thinking about how I would integrate it with the RPi GPIO code.

Python allows imports of random python code, so I used this to allow the GPIO code (lightSwitch.py) to call lightStatus.py with a function. I put the message in the function as a parameter. Clicking the button on a breadboard toggles a value between True and False. True and False are the message.

After some debugging I was able to press the button on the breadboard and see the messages appear on my computer monitor across the room. Time to geek out! The flow of electrons through a circuit trigger a message that travels around the world to change some tiny LED's on my monitor - and it was all pretty much free. Is this what the first telegraph seemed like?



### Heading 2

* Point 1
* Point 2
* Point 3

---
icon: raspberry-pi
---

# Paho MQTT RPi Client

<figure><img src="../.gitbook/assets/PiCloudTwin2.webp" alt=""><figcaption><p>A Raspberry Pi Cloud Connection Concept</p></figcaption></figure>

#### Why Use Paho?

Paho is an MQTT client implementation maintained by the Apache Foundation. There are libraries available to ease integrating it into several languages. These aspects make it a good choice for a project where multiple popular languages will be used. There are differences between the languages but a lot of similarity in the implementations.

The Paho library will be useful to connect the Raspberry Pi GPIO interface with an MQTT server because it is available as a [plugin for Python](https://pypi.org/project/paho-mqtt/). I built and ran it on a PC to get the server connection details ironed out before using it with the GPIO handler on the Pi.

#### Quick Start

<figure><img src="https://www.hivemq.com/_app/immutable/assets/tw-hmq-logo.BOcxywQK.svg" alt="" width="188"><figcaption></figcaption></figure>

[HiveMQ](https://www.hivemq.com/) provides [a number of different sample implementations](https://www.hivemq.com/mqtt/mqtt-client-library-encyclopedia/) including [one in Python](https://www.hivemq.com/blog/mqtt-client-library-paho-python/). I chose to use it as my starting point to create my message handler on my Pi, and named it lightStatus.py. Hive provides the configuration required to connect and communicate with their free cloud server. Hive also provides a [public server ](https://www.hivemq.com/demos/websocket-client/)that requires less setup than the free starter server instance I used. The free starter is serverless, and which - annoyingly - changes its name string periodically. After the name string is part of multiple configurations in more than a couple places it is better to look for a more permanent message broker or fall back on the public server.

After getting the code working on my dev machine, I put it in a GiT repo and moved over to the Pi. I started thinking about how I would integrate it with the GPIO code, but first I ran it. Then I had to read up on how Python compartmentalizes code.

I learned that Python allows imports of random python code, not just libraries. The GPIO code (lightSwitch.py) can import lightStatus.py and call a function in it. I put the message in the function call as a parameter. This made clicking the button on a breadboard toggle a value between True and False and also send a True or False message by adding a couple lines of code.&#x20;

The message "payload" is set to a hard value "true" in this weird instantiator. This method enables one to test the code directly -without it being a module import. and it still works as an import.

```python
if __name__ == '__main__':
    run("true")
```

Then I was able to press the button on the breadboard and see the messages appear on my dev machine browser from across the room! The flow of electrons through a circuit I wired up triggers a message that travels around the world to change some tiny LED's on my monitor - and it was all pretty much free. Is this what the first telegraph felt like?

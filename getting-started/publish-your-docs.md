---
icon: globe-pointer
---

# Architecture

Architecture

TrueTwin relies on several languages and server technologies to combine a physical device with a virtual one. The IoT MQTT standard for publishing and subscribing to events is the part that holds all the rest together.&#x20;

### MQTT Servers

Two different servers were chosen to provide the event signalling. One is HiveMQ, which is a free cloud-hosted service . The other is Mosquitto, which is a open project run locally. They can be used individually or at the same time.

#### Repo

The Repository Mosquitto Server contains the configuration details and other specific information about it.

#### Execution Environment

The server runs on a Linux PC on the same LAN as the rest of the project and is not accessible on the internet.

### Device(s)

For now, there is a single physical device used. It is a Raspberry Pi 4 outfitted with a breadboard containing a switch and an LED light. A Python program is running on the device that controls the LED light via the switch. This program calls on another that connects and sends a message to the MQTT server whenever the LED light changes (on and off).

#### Repo

Paho MQTT RPi Client

#### Execution Environment

Raspberry Pi device. The messaging client can execute on the Linux PC if the payload argument is replaced with a String literal value.

### VR Environment

Both Unity and Unreal Engine were explored for their ability to integrate in the TrueTwin project scenario. Unity won on the strength of its built-in ability to pass data back and forth to web browsers using the WebX standard.

#### Repo

Browser Data 2D

#### Execution Environment

The Unity runtime is contained in a web browser. A VR experience can be loaded in a headset via the browser.

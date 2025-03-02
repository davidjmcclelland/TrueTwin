---
icon: layer-group
---

# Architecture

TrueTwin relies on several languages and server technologies to combine a physical device with a virtual one. The IoT MQTT standard for publishing and subscribing to events is the part that holds all the rest together.

<figure><img src="../.gitbook/assets/digitalMaterial.webp" alt=""><figcaption></figcaption></figure>

### Sequence of Interactions

```mermaid
---
config:
  theme: false
  themeVariables:
    darkmode: false
    mainBkg: "#555"
    actorBkg: "#AAA"
    primaryBorderColor: "#555"
    labelTextColor: "#FFF"
    fontSize: "24px"
---
sequenceDiagram
  actor VR user
  participant Virtual as Virtual
  participant Broker
  participant Device as Device
  actor Touch user
  
  VR user ->> Virtual: toggle light off
  Virtual ->> Broker: lightswitch off 
  Broker ->> Device: lightswitch off
  Touch user ->> Device: toggle light on
  Device -->> Broker: lightswitch on
  Broker -) Virtual: lightswitch on

```

### Components and Responsibilities

#### Hardware

```mermaid

graph TD

  R:[Raspberry Pi 4] <--> B:[breadboard]
  N@{ shape: comment, label: "Hosts Python Code\nfor I/O and\nmessaging"}
  B:[breadboard] <--> U:[User Inputs]
  B:[breadboard] --> I:[Indicators]

```

Software

```mermaid
---
config:
  fontSize: 24px
  layout: elk
---
flowchart TD
 subgraph Python["Python"]
        P["(Python) paho-mqtt-rpi-client"]
        R["Raspberry Pi"]
        N["lightSwitch.py
for I/O and
lightStatus.py for messaging"]
  end
 subgraph subGraph1["Servers on Docker"]
        S["Message Broker"]
        W["HTTP Server Publishing WebXR"]
  end
 subgraph Unity["Unity"]
        XR["WebXR Export"]
        C["C# and Javascript code"]
  end
    R --> P
    P <--> S
    B["Browser"] <--> WS["Web Sockets"]
    WS <--> S
    C --> XR
    XR -.-> W
    W <--> B
    N@{ shape: comment}
```

### Message Brokers

Several message broker servers were chosen to test their event signalling capabilities, as well as their ease of configuration, maintenance and scalability. One is HiveMQ, which is a free cloud-hosted service . Another is Mosquitto, which is a self-hosted open source solution. Third is self-hosted RabbitMQ, which offers a different protocol while also supporting MQTT. I chose to run the self-hosted servers in docker containers on a seperate linux server.

### Web Server

Since the entire project environment is contained inside a LAN without internet access, the web server is almost an afterthought. The easiest way to host is to build the landing page from inside Unity. It will open the web page in a browser window automatically. A server sets the address to localhost and assigns a random port.

### Device(s)

For now, there is a single physical device used. It is a Raspberry Pi 4 outfitted with a breadboard containing a switch and an LED light. A Python program is running on the device that controls the LED light via the switch. This program calls on another that connects and sends a message to the MQTT server whenever the LED light changes (on and off).

### VR Environment

Both Unity and Unreal Engine were explored for their ability to integrate in the TrueTwin project scenario. Unity won on the strength of its built-in ability to pass data back and forth to web browsers using the WebX standard.

### Test/iteration tools

Before approaching the Raspberry Pi and Unity implementations it was important to test the servers to ensure that a stable, reproducible connection could be achieved at any time. An existing project (React MQTT) had already been used for this purpose. Additional MQTT clients were used from MQTT Client Examples (HiveMQ). These offered the convenience of running in a browser and displaying messages. The Mosquitto Server provides CLI-driven publish and subscribe clients that are useful for verifying that the server is running and responding.

[The list of projects used to build and support TrueTwin](https://github.com/stars/davidjmcclelland/lists/truetwin-project)

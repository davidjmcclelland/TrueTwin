---
icon: server
---

# MQTT Server

<figure><img src="../.gitbook/assets/trueTwinMQTT.webp" alt=""><figcaption></figcaption></figure>

Mosquitto server is a popular open-source messaging broker. It can be run from a cloud, on-prem, an internal server or even a Raspberry Pi SBC. There are more robust industrial servers that provide higher scale and availability levels using the same protocol. These are not within the scope of my project.

### Why use MQTT?

MQTT has been in use for over 10 years and is trusted by large process-control industries. It is among the simplest protocols for publishing and subscribing among devices. Messages consist of plain text, and are grouped into topics.  Devices subscribe to topics, so they only receive relevant messages. There are additional protocols for various aspects of message QOS and connection rules which are optional.

### Service Options

{% stepper %}
{% step %}
### HiveMQ Free Hosted Cloud

This service requires no server installation. It has limits designed to permit testing but prevents scaling up to commercial use, which [HiveMQ](https://www.hivemq.com/company/get-hivemq/) offers for a price. The only limitation that impacts testing is that the server endpoint is a generated string which changes periodically. This forces the developer to update the connection configuration for all publishers and subscribers, which becomes increasingly cumbersome as more components are built on. Another option is to spin up the free tier server on Docker or Kubernetes.
{% endstep %}

{% step %}
### Self-hosted Mosquitto Server

Installing and running Mosquitto server directly on any PC is not difficult. This approach was used to avoid the randomized endpoint names from HiveMQ. There is a download for clients to test publish and subscribe in CLI to ensure it is running.
{% endstep %}

{% step %}
### Mosquitto Docker Container

This method is preferred because it removes the need to install and manage the server, and allows for maintaining and managing the service in a visible dashboard environment. The same test clients work with this setup. I can spin up the container when I intend to demo.
{% endstep %}

{% step %}
### RabbitMQ Message Broker

RabbitMQ can run on any environment Mosquitto can. It supports more protocols than MQTT  such as AMQP. It claims to have more options to define how messages are published, such as routing, filtering, streaming and federation. It also supports acknowledgement and clustering. The software is open source, but is also offered as a service commercially.
{% endstep %}
{% endstepper %}


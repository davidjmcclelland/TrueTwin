---
icon: rabbit-running
---

# RabbitMQ Docker Container

Describe integration with AMQT

#### Installing RabbitMQ Docker Image

When installing RabbitMQ you must install with the administrator UI. This is an option that can be skipped by default. It is included in the docker run here:

```
// Docker
docker run -it --rm --name rabbitmq 
-p 5672:5672 -p 15672:15672 
rabbitmq:4.0-management
```

It is preferred to save the setup details in a yaml file and use Docker Compose to pull and install the image:

```yaml
version: '3'

services:
  rabbitmq:
    image: rabbitmq:management
    container_name: rabbitmq
    hostname: 'rabbit-1'
    environment:
      - RABBITMQ_DEFAULT_USER=username
      - RABBITMQ_DEFAULT_PASS=YoUrPaSsWoRd
    ports:
      - "5672:5672"
      - "15672:15672"
    restart: "always"
networks:
  default:
    driver: bridge
```

Once installed and running, the administration UI will be found at the specified port. The 15672 port is used for shttp connections.


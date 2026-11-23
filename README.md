# ⚙️ Config Server Repository

External **configuration repository** for my Spring Boot microservices. It is meant to be read by a **Spring Cloud Config Server**, so services get their settings from Git instead of from files packaged inside each JAR.

It holds the configuration for the `order-service` of my **[inter-service communication](https://github.com/LazaroDevelop/inter_service_communication)** microservices project.

## 📂 Contents
| File | Service | What it configures |
|------|---------|--------------------|
| `order-service.yml` | `order-service` | HTTP port (`8081`) and Eureka service registry location |

## 🧩 How it works
~~~text
  order-service  --(asks for its config)-->  Config Server  --(reads)-->  this Git repository
~~~
1. The **Config Server** is pointed at this repository.
2. When `order-service` starts, it asks the Config Server for the `order-service` configuration.
3. The Config Server serves the matching `order-service.yml` file from this repo.

## 🛠️ Use it from a Config Server
~~~yaml
# application.yml of the Spring Cloud Config Server
server:
  port: 8888

spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/LazaroDevelop/config-server-repository
          default-label: main
~~~

And in the client service:
~~~yaml
spring:
  application:
    name: order-service
  config:
    import: optional:configserver:http://localhost:8888
~~~

## 📝 Naming convention
Files follow the Spring Cloud Config convention `{application}-{profile}.yml`, for example `order-service.yml` (default profile) or `order-service-dev.yml` (dev profile).

## 👤 Author

**Lazaro Noel Guerra Medina**, Java Backend Engineer

> *"Make it work, make it right, make it fast."* ☕

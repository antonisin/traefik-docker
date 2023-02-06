# Traefik docker

## Author
 Maxim Antonisin <br>
[![img](https://img.shields.io/badge/email-maxim.antonisin%40gmail.com-blue?style=for-the-badge&logo=gmail)](mailto:maxim.antonisin@gmail.com)
[![img](https://img.shields.io/badge/linkedin-Maxim%20Antonisin-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/mantonishin/)
[![img](https://img.shields.io/badge/github-antonisin-blue?style=for-the-badge&logo=github)](https://github.com/antonisin)

## Requirements
[![img](https://img.shields.io/badge/docker-required-orange?style=for-the-badge&logo=docker)](https://getcomposer.org/download/)

## Description
This repository provides a simple and easy-to-update configuration for running Traefik on Docker. With these config 
files, you can quickly create and launch a Traefik Docker container to act as a reverse proxy and load balancer for your 
projects. The main purpose of this repository is to have a single entry point for all your projects, accessible on 
default ports (e.g. 80, 443), so you can manage them all in one place and easily add or modify them.

In other words, the Traefik Docker container acts as a central hub, listening on ports 80 and 443, and directing traffic
to other Docker containers running your various projects. This setup helps to avoid conflicts when running multiple 
containers on the same port and removes the need for including a port number in the URL.

Example: 
```
HTTP Request (project1.test) 80 -> traefik_container -> project_container_1 
HTTP Request (project2.test) 80 -> traefik_container -> project_container_2
```
or
```
Internet
|
|  Request to project1.test
|  ------------------------------->
|
|  Traefik Docker Container
|  ------------------------------->
|
|  Project 1 Docker Container
|  ------------------------------->
|
|  Response to User
|  <-------------------------------
```

## Installation
1. Clone this repository.
    ```shell 
    git clone <THIS_REPO_URL> 
   ```
2. Make sure that ports 80 and 443 are free.
3. Run docker-compose up -d
    ```shell 
    docker-compose up -d
   ```


## Usage
To create the connection and alias between a container and a domain or hostname, you need to add labels to your Docker 
Compose file for the relevant container/service. Here's an example:
```yaml
version: '3.7'
services:
    frontend:
        build: node:14.15.4-alpine
        expose: [ 3000 ]
        labels:
            - traefik.enable=true
            - traefik.http.routers.mavic-frontend.rule=Host(`frontend.test`)
            - traefik.http.services.mavic-frontend.loadbalancer.server.port=3000
      
```
In this example, we have a frontend service that is running on port 3000. To allow Traefik to route traffic to this 
service, we need to expose the port and add the relevant labels. The labels specify the domain name for the service, 
which can be replaced with any desired value.

## Support
<a href="https://www.buymeacoffee.com/maximusCode"> <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" height="50" width="210" alt="sleepwalker" style="margin-right: 12px;" /></a>
<a href='https://ko-fi.com/maximusCode' target='_blank'><img  height="50" width="210" src='https://cdn.ko-fi.com/cdn/kofi4.png?v=3' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
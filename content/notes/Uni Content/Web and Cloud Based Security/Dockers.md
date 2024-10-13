# Concepts

#docker #node-js #hypervisors

---
# Dockers
## Setting up a new Project

Suitable for backend
- nodeJS
- express API

DB
- MongoDB

Frontend
- Apache

## Docker vs Hypervisors

Hypervisors are mostly used to virtualise development

Dockers are mostly used to virtualise deployment

Dockers are small linux code
- They require some kind of operating system which can support a docker daemon

On top of this are the containers, which are a combination of the application and the libraries that the application needs

![|400](https://remnote-user-data.s3.amazonaws.com/jk2VlZNAUThsyyAyXhI4TN1x9VSB3QiEXneoUc1GG-sDZBhMWTAsbfRV_p2WPc79Ov09QaWvjjKsosZGJz6K3yMnfxaXlN0fsCnvxI_RuWRmyEtthEeEzLy-QUPiRbdc.png) 

## How Dockers Work

Both containers are run for frontend and backend

![|400](https://remnote-user-data.s3.amazonaws.com/sh7wDQ2GXuv-6t8yK3HMvqaDvums11KEpP3SJI-h1ksrWHlQ8sx75hoNDhgEDWwNKSzbcGwpV6L55-L04iYz8UpbZT93yuirhwqt3gvLi9NCDfvTztxW2kW7kQ5R8Zb_.png) 

## Container Contains

- Networking
- Processes
- Dependencies
- Code
- Config
 
## Service Delivery Platform

![|400](https://remnote-user-data.s3.amazonaws.com/MTphwWV8AuHmylEz2HsRkq6P2ySy6mK7dVJthH6CGwQupb-N4UKqPRiDJXRzwb4Oc2OU-dgkRRjMIF2uso8u6IZoh5JPycE_alZKGdwEHzMNn7d7zHK9ByX6EKXC6t01.png) 

The orchestration helps manage a large number of docker containers at once
 
## With One Container

- Help dockers discover each other and other services
- Allocate resources
- You can start, stop and restart containers if they fail
 
## Docker Vulnerabilities
### Software Vulnerability

Container Escape - The attacker gains full control of the host and can try to attack resources in the internal network segment
- This can allow the attacker to deploy a malicious container inside the production environment


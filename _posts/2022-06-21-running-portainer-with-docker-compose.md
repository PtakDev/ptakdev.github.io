---
title: Running Portainer with docker-compose
date: 2022-06-21 18:20:00 +0100
categories: [Docs, Portainer]
tags: [portainer, docker, docker-compose, ubuntu 20.04 ]     # TAG names should always be lowercase
---

## docker-compose.yaml

```yaml
version: '3.3'
services:
  portainer:
    # You can change the tag `latest` to a specific version ex. `2.13.1`
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: unless-stopped
    ports:
      # Expose HTTP port if required
      # - 9000:9000
      # Expose a TCP tunnel server over port 8000
      # - 8000:8000
      - 9443:9443
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      # Change ./portainer-data to directory where you want to keep portainer data on local machine
      - ./portainer-data:/data
```
> After running a Pontainer for the first time you will have to create a admin user. 
{: .prompt-info }

> To access your Portainer Server please use HTTPS protocol. Example: [`https://localhost:9443`](https://localhost:9443){:target="_blank"}
{: .prompt-tip }


References

[`Portainer Community Edition image`](https://hub.docker.com/r/portainer/portainer-ce){:target="_blank"}
[`Portainer Documentation`](https://docs.portainer.io/start/install/server/docker/linux){:target="_blank"}
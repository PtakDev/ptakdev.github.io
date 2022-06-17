---
title: Running Jenkins in Docker with Docker Compose
date: 2022-06-17 10:30:00 +0100
categories: [Docs, Jenkins]
tags: [jenkins, docker, docker-compose, ubuntu 20.04]     # TAG names should always be lowercase
---

> I recomend to read the full guide published on CloudBees blog [How to Install and Run Jenkins With Docker Compose](https://www.cloudbees.com/blog/how-to-install-and-run-jenkins-with-docker-compose){:target="_blank"}
{: .prompt-info }

> If you trying to run any of the shell commands and you are getting `failed: Permission denied`, just put `sudo` in front of the command you are trying to run.
{: .prompt-tip }


## Create docker compose file

To retain all data even when the container is stopped, started, or deleted, we need to create an explicit volume for it. 

```yaml
version: '3.3'
services:
  jenkins:
    image: jenkins/jenkins:latest
    privileged: true
    user: root
    ports:
      - 8080:8080
      - 50000:50000
    container_name: jenkins
    volumes:
      - /home/${myname}/jenkins_compose/jenkins_configuration:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
```
{: file="docker-compose.yaml" }

> Change `/home/${myname}` to your user’s home directory or the path you created the new directory in.
{: .prompt-warning }

`/home/${myname}/jenkins_compose/jenkins_configuration` is mapped to `/var/jenkins_home` in the container. 


## Run Jenkins controller

 ```shell
 docker-compose up -d
 ```

 When creating Jenkins it's done, you can open Jenkins site in your browser. If you are running it in you local environment it should be [localhost:8080](localhost:8080){:target="_blank"}


## Initial Jenkins configuration

Follow the instructions on the browser screen to: 

* ### Unlock Jenkins

Print the password in the console without having to exec into the container by executing one of below commands command:

```shell
sudo docker exec ${CONTAINER_ID or CONTAINER_NAME} cat /var/jenkins_home/secrets/initialAdminPassword
```
```shell
docker logs jenkins | less
```
* ### Install suggested plugins

* ### Create the first admin user


## Add Jenkins Agent and define it

### Generate an SSH key

Two files are going to be generated executing below command; `jenkins_agent`, with the `private key`, and `jenkins-agent.pub`, with the `public key`.

```shell
ssh-keygen -t rsa -f jenkins_agent
```
{: file="~/jenkins_compose" }

Copy private key.

```shell
cat jenkins_agent
```
{: file="~/jenkins_compose" }

### Add credentials

##### Step 1. In our Jenkins Dashboard, we need to navigate to `Manage Jenkins`  &rarr; `Manage Credentials`.
##### Step 2. Here under `Store` click `Jenkins`.
##### Step 3. Now under `Domain` click `Global credentials (unrestricted)`.
##### Step 4. Select `Add credentials`.
##### Step 5. Set these options on this screen.

1. Select `SSH Username with private key`.
2. Limit the scope to System. This means the key can’t be used for jobs.
3. Give the credential an ID.
4. Provide a description.
5. Enter `jenkins` for a `username`. Don’t use the username used to create the key.
6. Under Private Key,  check `Enter directly`.
7. Paste the contents of `jenkins_agent` in the text box.

### Set up the agent

##### Step 1. Get the contents of the jenkins_agent.pub.
```shell
cat jenkins_agent.pub
```
{:file="~/jenkins_compose"}

##### Step 2. Stop Jenkins.
```shell
docker-compose down
```

##### Step 3. Add a agent to docker-compose.
```yaml
version: '3.3'
services:
  jenkins:
    image: jenkins/jenkins:latest
    privileged: true
    user: root
    ports:
      - 8080:8080
      - 50000:50000
    container_name: jenkins
    volumes:
      - /home/${myname}/jenkins_compose/jenkins_configuration:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
  agent:
    image: jenkins/ssh-agent:jdk11
    privileged: true
    user: root
    container_name: agent
    expose:
      - 22
    environment:
      - JENKINS_AGENT_SSH_PUBKEY=<JENKINS_AGENT.PUB_CONENTS>
```
{:file="docker-compose.yaml"}

> Replace `<JENKINS_AGENT.PUB_CONENTS>` with the contetnts of `jenkins_agent.pub` file.
{: .prompt-tip }

##### Step 4. Run Jenkins
Make sure you are in the directory that contains right `docker-compose.yaml` file.

 ```shell
 docker-compose up -d
 ```

> To check if the Jenkins controller and agent are running you can execute `docker ps` command. You should be able to see our containers lister there.
{: .prompt-tip }


### Define new Jenkins agent

###### Step 1. In our Jenkins Dashboard, we need to navigate to `Manage Jenkins`  &rarr; `Manage Nodes and Clouds` and click `New Node`.
###### Step 2. Give your agent a `name` and set the Remote `root directory` to `/home/jenkins/agent`.
###### Step 3. In the next part of the form under `Usage`, select `Use this node as much as possible`.
###### Step 4. Under `Launch method`, select `Launch agents via SSH`.
###### Step 5. For `Host`, enter `agent`.
###### Step 6. Under `Credentials`, select the one created earlier.
###### Step 7. Under `Host Key Verification Strategy`, select `Non verifying Verification Strategy`.
###### Step 8. Click `Advanced` on the right.
###### Step 9. Set the `JavaPath` to `/opt/java/openjdk/bin/java`.
###### Step 10. Click `Save`.

To verify if the Agent is successfully connected and online go to Log and look for output `Agent successfully connected and online`.

> I came across an Error `Agent JVM has terminated. Exit code=127 docker` while trying to run the agent. I had to get inside of the jenkins container and get the java path. To get inside the container execute `docker exec -it <CONTAINER_NAME> bash`, and inside of the container execute `whereis java`. Copy the path and edit `JavaPath` from Step 9. To close the container shell type `exit`.
{: .prompt-tip }


# Everything is now up and running!

> It's highly advisable to **not** run any builds on the built-in node, instead using `agents` to run builds. To prevent builds from running on the built-in node directly, navigate to `Manage Jenkins` &rarr; `Manage Nodes and Clouds`. Select `Built-In Node` in the list, then select `Configure` in the menu. Set the `number of executors` to `0` and save.
{: .prompt-tip }

## Reference:

[`How to Install and Run Jenkins With Docker Compose`](https://www.cloudbees.com/blog/how-to-install-and-run-jenkins-with-docker-compose){:target="_blank"}
[`Jenkins Docker image`](https://hub.docker.com/r/jenkins/jenkins/){:target="_blank"}
[`Jenkins Docker documentation`](https://github.com/jenkinsci/docker/blob/master/README.md){:target="_blank"}
[`Using Jenkins agents`](https://www.jenkins.io/doc/book/using/using-agents/){:target="_blank"}
[`Controller Isolation`](https://www.jenkins.io/doc/book/security/controller-isolation/){:target="_blank"}
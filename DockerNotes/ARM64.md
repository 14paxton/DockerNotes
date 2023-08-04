---
title: ARM64
permalink: DockerNotes/ARM64
category:  DockerNotes
parent:   DockerNotes
layout: default
has_children: false
share: true
shortRepo:
  - dockernotes
  - default          
---


<br/>          

<details markdown="block">                
<summary>                
Table of contents                
</summary>                
{: .text-delta }                
1. TOC                
{:toc}                
</details>                

<br/>                

***                

<br/>
# cli build
```shell
docker build --platform linux/arm64  .
```
# cli run
```shell
docker run --platform linux/arm/v8 dbmigration:1.1
```

## all platforms
```shell
docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t username/demo:latest --push .
```

# add to from
```shell
FROM --platform=linux/x86_64 $REGISTRY_HOST/guardian/base-images/node16-builder:1.0.0 as builder
```

# Add this snipped to your ~/.zshrc and ~/.bashrc. It allows you not to repeat the flag anytime you perform a docker run command:

> useful only for Mac OS Silicon M1, 
 
> still working but useless for the other platforms

```shell
docker() {
  if [[ `uname -m` == "arm64" ]] && [[ "$1" == "run" || "$1" == "build" ]]; then
     /usr/local/bin/docker "$1" --platform linux/amd64 "${@:2}"
  else
     /usr/local/bin/docker "$@"
  fi
}
```

You can set the environment variable DOCKER_DEFAULT_PLATFORM:
```shell
export DOCKER_DEFAULT_PLATFORM=linux/amd64
```

# you can add in your docker-compose.yaml:
```yaml
services:
  service_name:
    environment:
      - DOCKER_DEFAULT_PLATFORM=linux/amd64
```

# add to build as env 
```shell
DOCKER_DEFAULT_PLATFORM=linux/amd64 docker-compose build
```
> Keep in mind that if you've already downloaded the image for a different platform, docker will keep using that image no matter what platform you specify as your default, you would delete the image using docker image rm your_img first to fix that.

# Alternatively, in the Dockerfile, include the following flag in the FROM command (for a multi-stage Dockerfile build, the flag is only needed for the first stage):

```shell
FROM --platform=linux/amd64 python:3.7-alpine
```

# For building images as part of a docker-compose build, include the platform: linux/amd64 for each service. For example:
```yaml
  services:  
    frontend:  
      platform: linux/amd64
      build: frontend  
      ports:
        - 80:80  
      depends_on:
        - backend  
    backend:  
      platform: linux/amd64
      build: backend 
```

# Debian ARM

```shell
  FROM        aemdesign/tini:debian-arm

LABEL   os="debian 8 arm" \
        container.description="oracle jdk" \
        version="jdk8" \
        maintainer="devops <devops@aem.design>" \
        imagename="oracle-jdk" \
        test.command=" java -version 2>&1 | grep 'java version' | sed -e 's/.*java version "\(.*\)".*/\1/'" \
        test.command.verify="1.8"


ARG JAVA_VERSION="8"
ARG JAVA_VERSION_TIMESTAMP="2133151"
ARG JAVA_DOWNLOAD_URL="https://www.oracle.com/au/java/technologies/javase-jdk${JAVA_VERSION}-downloads.html"
ARG JDK_DRIVEID="xxx"

ENV JAVA_HOME=/opt/jdk1.8.0_321/

COPY gdrive.sh .

RUN \
    echo "DOWNLOAD JDK DONE" && \
    bash ./gdrive.sh "download" "${JDK_DRIVEID}" "/opt/jdk.tar.gz" && \
    echo "INSTALL JDK" && \
    cd /opt/ && \
    tar -xvzf jdk.tar.gz && \
    export JAVA_HOME=${JAVA_HOME}  && \
    update-alternatives --install /usr/bin/java java ${JAVA_HOME%*/}/bin/java 1 && \
    update-alternatives --install /usr/bin/javac javac ${JAVA_HOME%*/}/bin/javac 1 && \
    update-alternatives --config java && \
    rm -rf /opt/jdk.tar.gz
```
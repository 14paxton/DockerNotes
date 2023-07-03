Where ubuntu for windows resides -
**[C:\\Users\\bpaxton\\AppData\\Local\\Packages\\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\\LocalState\\rootfs]{.underline}**

-   **Docker ps -a**

    -   show docker containers

-   **docker rm \$(docker ps -a -q -f status=exited)**

    -   remove all exited containers

        -   docker container prune

-   docker pull = copies images to docker host

-   docker rmi = removes images from docker host

-   docker ps = lists running containers

-   docker stop = stops running containers

-   docker rm = removes containers

-   **get docker ip =** docker-machine ip default

-   **docker ip for container =**

> **docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}"
> \[containter\]**

-   **get ports for container= docker port \[container\]**

-   **build image =** docker image build -t \[path to app with
    Dockerfile\].

-   **start container =**

> docker container run -d \--name \[choose name\] -p \[choose
> port\]:8080 \[imagename\]
>
> docker container run -it(interactive mode) alpine sh(shell)
>
> \[switch to windows containers\] docker container run -d \--name web1
> -p 80:80 microsoft/iis

-   exit container shell = ctrl + p + q

-   execute commands = docker container exec -it \[name/id\] ls
    /usr/share/nginx/html

# Dockerfile

FROM: 
    `Initializes a new build stage and sets the Base Image`

RUN: 
    `Will execute any commands in a new layer`

CMD: 
    `Provides a default for an executing container. There can only be
        one CMD instruction in a Dockerfile`

LABEL: 
    `Adds metadata to an image`

EXPOSE: 
    `Informs Docker that the container listens on the specified
        network ports at runtime`

ENV: 
    `Sets the environment variable \<key\> to the value \<value\>`

ADD: 
    `Copies new files, directories or remote file URLs from \<src\> and
        adds them to the filesystem of the image at the path \<dest\>.`

COPY: 
    `Copies new files or directories from \<src\> and adds them to the
        filesystem of the container at the path \<dest\>.`

ENTRYPOINT: 
    `Allows for configuring a container that will run as an
        executable`

VOLUME: 
    `Creates a mount point with the specified name and marks it as
        holding externally mounted volumes from native host or other containers`

USER: 
    `Sets the user name (or UID) and optionally the user group (or GID)
        to use when running the image and for any RUN, CMD,
        and ENTRYPOINT instructions that follow it in the Dockerfile`

WORKDIR: 
    `Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY,
        and ADD instructions that follow it in the Dockerfile`

ARG: 
    `Defines a variable that users can pass at build-time to the builder
        with the docker build command, using the \--build-arg
        \<varname\>=\<value\> flag`

ONBUILD: 
    `Adds a trigger instruction to the image that will be executed
        at a later time, when the image is used as the base for another build`

HEALTHCHECK: 
    `Tells Docker how to test a container to check that it is
        still working`

SHELL: 
    `Allows the default shell used for the shell form of commands to
        be overridden`

## CREATE DOCKER HUB IMAGE

### Docker Push:
    ```bash
        docker image push <USERNAME><IMAGE_NAME>:<TAG>
    ```
### Creating an image for Docker Hub:

    ```bash
        docker image tag <IMAGE_NAME>:<TAG>
    ```

###  Set up your environment:

    ```bash
        cd docker_images

        mkdir dockerhub

        cd dockerhub
    ```
    
###  Create the Dockerfile:

    ```bash
    
        vim Dockerfile
    ```
    
        > Dockerfile contents:
            ```
                \# Create an image for the weather-app using multi-stage build

                FROM node AS build

                RUN mkdir -p /var/node/

                ADD src/ /var/node/

                WORKDIR /var/node
                
                RUN npm install
                
                FROM node:alpine
                
                ARG VERSION=V1.1
                
                LABEL org.label-schema.version=\$VERSION
                
                ENV NODE_ENV=\"production\"

                COPY \--from=build /var/node /var/node
                
                WORKDIR /var/node
                
                EXPOSE 3000
                
                ENTRYPOINT \[\"./bin/www\"\]
                
                Git the weather-app code:
                
                git clone https://github.com/linuxacademy/content-weather-app.git src
                
                Use the Git commit hash as the image tag:
                
                cd src
                
                git log -1 \--pretty=%H
                
                cd ../
          
            ```
  
###  Build the image:

    ```bash
    
        docker image build -t <USERNAME>weather-app:<HASH> --build-arg
        VERSION=1.5 .
        
        Tag the image before pushing it to Docker Hub:
        
        docker image tag linuxacademy/weather-app:<HASH>
        <USERNAME>weather-app:<HASH>
        
    ```

###  Push the image to Docker Hub:

    ```bash
        docker login
        
        docker image push <USERNAME>weather-app:<HASH>
        
        Tag the latest image:
        
        docker image tag <USERNAME>weather-app:<HASH>
        <USERNAME>/weather-app:latest
    
    ```

###  Push the latest image to Docker Hub:

    ```bash
        
        docker login <USERNAME>
        
        docker image push <USERNAME>weather-app:latest
    ```

# Docker Compose

-   INSTALL

-   Download the latest version of Docker Compose:

-   sudo curl -L
    \"https://github.com/docker/compose/releases/download/1.23.2/docker-compose-\$(uname
    -s)-\$(uname -m)\" -o /usr/local/bin/docker-compose

-   Apply executable permissions:

-   sudo chmod +x /usr/local/bin/docker-compose

-   Test Docker Compose:

-   docker-compose \--version

    -   

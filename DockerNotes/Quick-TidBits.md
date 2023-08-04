---
title: Quick-TidBits
permalink: DockerNotes/Quick-TidBits
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
# Restart Docker
1) sudo su
   systemctl start docker
   systemctl enable docker
   systemctl restart docker
2) sudo dockerd
3) snap stop docker
   snap start docker
4) sudo systemctl unmask docker
   sudo systemctl start docker   


# To keep your Docker images small, don't install unnecessary editors. You can edit the files over SSH from the Docker host to the container:
       vim scp://remoteuser@containerip//path/to/document
       
# Use host ip
<a href="https://gist.github.com/14paxton/fc9331557d823620d73d15c453b83bd8" > Use Host IP yml </a>
    
    host.docker.internal
    The gateway is also reachable as gateway.docker.internal
    
    If you are running this stack on Linux you need to have the DOCKER_GATEWAY_HOST environment variable set for the Docker gateway host. Simply put this       line into your .bashrc (.bash_profile or .zshrc):
    export DOCKER_GATEWAY_HOST=172.17.0.1
    
    source https://docs.docker.com/desktop/mac/networking/.  
    
    extra hosts https://docs.docker.com/compose/compose-file/#extra_hosts
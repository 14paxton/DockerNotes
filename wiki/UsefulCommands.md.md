
# stop all containers:
```bash 
docker kill $(docker ps -q)
```

# remove all containers
```bash
docker rm $(docker ps -a -q)
```

# remove all docker images
```bash
docker rmi $(docker images -q)
```

# get container ip
```shell
sudo docker container inspect container_name_or_ID
```

> Don't know the container's name or ID? Use the command 

```shell
sudo docker ps
```
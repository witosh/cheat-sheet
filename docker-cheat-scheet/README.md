# Docker cheat sheet - a couple useful commands using dokcer

## Table of Contents
| Commands |  Projects and topics | 
| -------------| -------------|
|[*Manage docker images*](#manage-docker-images)|[*Manage Docker as a non root user*](#manage-docker-as-a-non-root-user)|
|[*Manage docker containers*](#manage-docker-containers)|[*Setup insecure registry on local docker*](#setup-insecure-registry-on-local-docker)|
|[*Manage docker volume*](#manage-docker-volume)|[Create own docker image](https://github.com/witosh/docker-cheat-sheet/tree/master/create-own-docker-image)|
|[*Manage docker compose*](#manage-docker-compose)|[Tomacta on docker](https://github.com/witosh/docker-cheat-sheet/tree/master/docker-tomcat)|
|[*Manage docker swarm*](#manage-docker-swarm)|[Jenkins on decker](https://github.com/witosh/learn-by-examples/blob/master/continuous-delivery/jenkins-on-docker/README.md#how-to-run-jenkins-on-docker)|

# Manage docker images

### Build image
- [docker build](https://docs.docker.com/engine/reference/commandline/build/) - build/create an image from Dockerfile
- [docker-compose build](https://docs.docker.com/compose/reference/build/) - rebuild or create docker images

### Remove images
- [docker image prune](https://docs.docker.com/engine/reference/commandline/image_prune/) - remove unused imges
- [docker rmi <image_name>](https://docs.docker.com/engine/reference/commandline/rmi/) - remove an image
- [docker rmi $(docker images -q)](https://docs.docker.com/engine/reference/commandline/rmi/) - remove all images based on ID
- [docker rmi $(docker images -q | head -n +2)](https://docs.docker.com/engine/reference/commandline/rmi/) - remove 2 recently created images based on ID
- [docker rmi $(docker images -q | tail -n +2)](https://docs.docker.com/engine/reference/commandline/rmi/) - remove 2 the most oldest created images based on ID

### Show images
- [docker images](https://docs.docker.com/engine/reference/commandline/images/) - show all images
- [docker images -q](https://docs.docker.com/engine/reference/commandline/images/) - show all images ID

**[⬆ Back to Top](#table-of-contents)**

# Manage docker containers

### Start/Stop conatiner
- [docker run](https://docs.docker.com/engine/reference/commandline/run/) - create container from image and start
- [docker run -d](https://docs.docker.com/engine/reference/commandline/run/) - create container from image and start in detached mode
- [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) - stop running container
- [docker start](https://docs.docker.com/engine/reference/commandline/start/) - starts stopped container
- [docker restart](https://docs.docker.com/engine/reference/commandline/restart/) - restart docker container container 
- [docker start $(docker container ls -a -q --filter name=<container_name>)](https://docs.docker.com/engine/reference/commandline/start/) - start container by given name
- [docker run -p 8080:80](https://docs.docker.com/engine/reference/commandline/run/) - map 8080 port of host to port 80 of container (now container will be available under localhost:8080)
- [docker run -p 8080:80 -p 8081:80](https://docs.docker.com/engine/reference/commandline/run/) - multiple map (now container is available under two ports)
- [docker run --name <new_container_name>](https://docs.docker.com/engine/reference/commandline/run/) - setup name of container

### Show containers info
- [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) - shows running/active containers
- [docker ps -format="ID\t{{.ID}}\nNAME\t{{.NAME}}"](https://docs.docker.com/engine/reference/commandline/ps/) - shows running/active containers in formatted way
- [sudo docker ps --format "{{.ID}}: {{.Image}} {{.Names}}"](https://docs.docker.com/engine/reference/commandline/ps/) - shows running/active containers in specific format
- [docker ps -a | grep Exit](https://docs.docker.com/engine/reference/commandline/container_ls/) - show only stopped containers
- [docker ps --no-trunc](https://docs.docker.com/engine/reference/commandline/ps/) show the full command along with the other details of the running containers
- [sudo docker ps --format "{{.ID}}: {{.Image}} {{.Names}}"](https://docs.docker.com/engine/reference/commandline/ps/) - show active container in specific defined format
- [docker ps -a --filter volume=<name_of_docker_volume>](https://docs.docker.com/engine/reference/commandline/ps/) - show which container is applied to specific volume


- [docker container ls -a](https://docs.docker.com/engine/reference/commandline/container_ls/) - show stopped and running containers (all the containers)
- [docker container ls -a -q](https://docs.docker.com/engine/reference/commandline/container_ls/) - show ID stopped and running containers (all the containers)
- [docker container ls -f status=exited -a](https://docs.docker.com/engine/reference/commandline/container_ls/) - shows only stopped containers

### Show container logs
- [docker logs container-id](https://docs.docker.com/engine/reference/commandline/container_logs/) - shows logs of running container

### Execute command on container
- [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) - execute command within running container
- [sudo docker exec -it <name_or_container_id> bash](https://docs.docker.com/engine/reference/commandline/exec/) - access a shell and run custom commands inside a container
- [sudo docker exec -it <name_or_container_id> cat <path/to/chosen/container/resource>](https://docs.docker.com/engine/reference/commandline/exec/) - show data inside docker container
- [sudo docker exec -it <name_or_container_id> ls -lrt <path/to/chosen/container/directory>](https://docs.docker.com/engine/reference/commandline/exec/) - show the content of the /<path/to/chosen/container/directory> directory inside the docker conatiner
- [docker cp <local_catalogue>:<inner_container_data_volume>](https://docs.docker.com/engine/reference/commandline/cp/) - copy volume inside a container and extract the data

### Kill container
- [docker kill](https://docs.docker.com/engine/reference/commandline/kill/)  - kill a container

### Remove containers
- [docker container rm](https://docs.docker.com/engine/reference/commandline/container_rm/) remove container
- [docker container rm $(docker container ls -a -q)](https://docs.docker.com/engine/reference/commandline/container_rm/) remove all containers

**[⬆ Back to Top](#table-of-contents)**

# Manage docker volume

### Create dokcer volume
- [docker volume create](https://docs.docker.com/engine/reference/commandline/volume_create/) - create docker volume
- [docker volume create -name](https://docs.docker.com/engine/reference/commandline/volume_create/) - create docker volume with specific name

### Remove docker volume
- [docker volume prune](https://docs.docker.com/engine/reference/commandline/volume_prune/) - remove unused docker volumes

### Shows docker volume
- [docker volume ls](https://docs.docker.com/engine/reference/commandline/volume_ls/)- shows all local volumes
- [docker ps -a --filter volume=<name_of_docker_volume>](https://docs.docker.com/engine/reference/commandline/ps/) - show which container is applied to specific volume

### Remove docker volume
- [docker volume rm](https://docs.docker.com/engine/reference/commandline/volume_rm/) -remove docker volume

### Docker volume in use
- [docker run <container_id> --volumes-from <another_container_id>](https://docs.docker.com/engine/reference/commandline/run/) - run docker container with shared volume of another container

**[⬆ Back to Top](#table-of-contents)**

# Manage docker network

### Create docker network
- [docker network create](https://docs.docker.com/engine/reference/commandline/network_create/) - create network based on name

### Shows networks
- [docker network ls](https://docs.docker.com/engine/reference/commandline/network/) - shows all networks

### Remove docke network
- [docker network prune](https://docs.docker.com/engine/reference/commandline/network_prune/)  - remove unused docker networks
- [docker network rm](https://docs.docker.com/engine/reference/commandline/network_rm/) - remove docker network

**[⬆ Back to Top](#table-of-contents)**

# Manage docker compose

### Start/Stop docker-compose
- [docker-compose up](https://docs.docker.com/compose/reference/up/)   starts containers
- [docker-compose down](https://docs.docker.com/compose/reference/down/)   stop containers 
- [docker-compose restart](https://docs.docker.com/compose/reference/restart/) - restart docker continer base on name of container 

### Show docker-compose containers
- [docker-compose ps](https://docs.docker.com/compose/reference/ps/) - shows running containers by docker-compose

### Show docke -compose logs
- [docker-compose logs <container_name>](https://docs.docker.com/compose/reference/logs/) - shows container logs based on name of service
- [docker-compose logs -f](https://docs.docker.com/compose/reference/logs/) - shows container logs follow logs
- [docker-compose logs -f --tail 100](https://docs.docker.com/engine/reference/commandline/logs/) - shows application logs with a last 100 lines
- [docker-compose logs -f <service>](https://docs.docker.com/engine/reference/commandline/logs/) - shows logs of a specific service
- -d flags avoid to show all logs started services

### Pull images for docker-compose 
- [sudo docker-compose pull --parallel]() - pulling multiple docker images at once defined in docker-compose file

**[⬆ Back to Top](#table-of-contents)**

# Manage docker swarm

### Restat container in swarm
The scale command enables you to scale one or more replicated services either up or down to the desired number of replicas.
- [sudo docker service scale <service_name>=0](https://docs.docker.com/engine/reference/commandline/service_scale/) - down replicated service inside swarm node
- [sudo docker service scale <service_name>=1](https://docs.docker.com/engine/reference/commandline/service_scale/) - up replicated service inside swarm node

### Update new service
- [sudo docker service update --image <image_name> <service_name>]() - update new version of service on docker swarm

### Show container logs
- [sudo docker service logs -f <container_name_or_id>]() - shows logs of container
- [sudo docker service ls](https://docs.docker.com/engine/reference/commandline/logs/) - shows started containers on swarm

### Show swarm containers
- [sudo docker service ps](https://docs.docker.com/engine/reference/commandline/service_ps/) List the tasks of one or more services
- [sudo docker service ps --no-trunc](https://docs.docker.com/engine/reference/commandline/service_ps/) show the full command along with the other details of the running containers

**[⬆ Back to Top](#table-of-contents)**

# Manage Docker as a non root user

[Running docker localy without sudo](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)

**[⬆ Back to Top](#table-of-contents)**

# Setup insecure registry on local docker

1. Go into the path on your local computer:
```bash
/etc/docker/daemon.json
```
2. Open deamon.json in text editor and setup content:
```bash
{
    "insecure-registries" : [ "hostname.cloudapp.net:5000" ]
}
```

3. Restart docker.
```bash
sudo systemctl restart docker
```

**[⬆ Back to Top](#table-of-contents)**


Sources: 
- [Docker cheat-sheet](https://github.com/wsargent/docker-cheat-sheet)

- [Docker architecture](https://docs.docker.com/engine/docker-overview/)


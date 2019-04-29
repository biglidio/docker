# Docker basic commands

## How to run a docker container? 

//Run a docker container from an image
docker run <image>

//List docker containers
docker ps

//List all docker containers, even the ones are not running.
docker ps -a

//Run a container by terminal 
docker run -ti <image> bash

//List docker images
docker images

//CTRL + P + Q = Right way to get out from container

//CTRL + D = Get out stopping your container

//Enter in a container terminal
docker attach <container>

//Container informations
docker stats <container>

//Access container processes
docker top <container>

//Access container logs
docker logs <container>

//Remove a container, -f to stop before removing
docker rm <container>
docker rm <container> -f

//Remove all containers, running or not
docker rm $(docker ps -a) -f

//Run container with limited memory
docker run -ti --memory 512m --name <container> <image>

//Verify conatiner memory configuration
docker inspect <container> | grep -i mem

//Update container memory limit
docker update -m 512m <container>

//Run container with cpu limited
docker run -ti --cpu-shares 1024 --name <container> <image>

//Update container cpu limit
docker update --cpu-shares 512 <container>

//Run container with volume
docker run -ti -v <path_container> <image> /bin/bash

//Run container with volume from host
docker run -ti -v <path_host>:<path_container> <image>

//Run container binding host port, giving name, mounting volume from other container and setting environments variables
docker run -d -p <port>:<port> --name <container> --volumes-from <container> -e <env_var1> -e <env_var2> -e <...>

//Build a docker image
docker build -t <image>:<version> <path>

//Remove all docker containers
docker rm $(docker ps -a -q) -f

//Remove all docker images
docker rmi $(docker images -q) -f

//Login to Docker HUB account
docker login -u <user>

//Push your image to Docker HUB
docker push <user>/<image>:<version>

# Dockerfile configuration

//Set to start from a docker image
FROM <image>

//About the image mantainer
MANTAINER <name>

//Add file into container
ADD file <path_host>
COPY file <path_host>

//Entrypoint parameters (default entrypoint is bash, but could be a dump)
CMD ["sh", "-c", "echo", "$HOME"]

//Description about the image
LABEL Description="Blablabla"

//Where to start running
ENTRYPOINT ["/usr/bin/apache2ctl", "-D", "FOREGROUND"]

//Environment variables
ENV var="value"

//Open ports
EXPOSE 80

//Each RUN line create a new docker layer
RUN command_layer1 && command_layer1 && command_layer1 &&
RUN command_layer2 && command_layer2 && command_layer2 &&

//The UNIX user inside the container
USER user_name (root)

//Root path
WORKDIR <path_container>

//Set volumes inside the container
VOLUME <path_container>
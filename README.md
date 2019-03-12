D-NOTE-BCC
----------

create docker image from git repo
    $ docker build -t docker-d-note-bcc .

deploy that image
    $ docker run --detach --volume /srv/dnote:/dnote --publish 8080:8080 --name dnote docker-d-note-bcc

hit : localhost:8080 

(if you need to rebuild remove old image then run build command)


if docker failes to run, then 

Clean Docker 
--------------

delete volumes
// see: https://github.com/chadoe/docker-cleanup-volumes

$ docker volume rm $(docker volume ls -qf dangling=true)
$ docker volume ls -qf dangling=true | xargs -r docker volume rm

delete networks

$ docker network ls  
$ docker network ls | grep "bridge"   
$ docker network rm $(docker network ls | grep "bridge" | awk '/ / { print $1 }')

remove docker images

// see: http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images

$ docker images
$ docker rmi $(docker images --filter "dangling=true" -q --no-trunc)

$ docker images | grep "none"
$ docker rmi $(docker images | grep "none" | awk '/ / { print $3 }')

remove docker containers

// see: http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images

$ docker ps
$ docker ps -a
$ docker rm $(docker ps -qa --no-trunc --filter "status=exited")






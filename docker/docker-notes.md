# Docker Notes

## Running Containers

### Interactive container
run a container and log in within its shell.  
-it stands for i-interactive, -t terminal, sh for shell  
  `sudo docker container run -it alpine:3.4 sh`

### Making containers persist
`docker container run -idt schoolofdevops/loop program`  
  idt is deattached container.
program is an app/program which is persistant (loop in this case)  
ie something that does not finish, so container is alive.  

### All processes inside a container
when in a container you can do ps aux to see all processes running in it  
a = show processes for all users  
u = display the process's user/owner  
x = also show processes not attached to a terminal  
`ps aux`

## Listing containers

list running containers  
`docker container ps`

list last container  
`docker container ps -l`

list last 2 Containers  
`docker container ps -n 2`

list all containers  
`docker container ps -a`

## Logs of container

if container is running in deattached mode you can view logs as:  
  `docker logs CONTAINER_ID`  
  `docker logs CONTAINER_NAME`  

add -f to get updated logs (continuous stream of logs)  
  `docker logs -f CONTAINER_ID`  
  `docker logs -f CONTAINER_NAME`  

## Pause/Unpause

`docker container pause CONTAINER_ID`  
`docker container unpause CONTAINER_ID`  

## Stop

`docker container stop CONTAINER_ID`  
`docker container start CONTAINER_ID`  

## Docker System Command
~~~~

Usage:  docker system COMMAND

Manage Docker

Commands:
  df          Show docker disk usage
  events      Get real time events from the server
  info        Display system-wide information
  prune       Remove unused data

Run 'docker system COMMAND --help' for more information on a command.
~~~~

## Ports:

-P for enabling a port mapping from host to reach the container.  
if no ports provided on host it uses 32768 fron host (or onwards if this one is used)
and 80 on container
`docker container run -idt -P schoolofdevops/vote`  

eg -P 8080:80 where 8080 is host port and 80 is container port.  
`docker container run -idt -p 8080:80 schoolofdevops/vote`   

to access the application do IP:portonhost eg 0.0.0.0:32768

## Rename
docker container rename name new_name  
`docker container rename jobial_goldberg jack_the_ripper`  

## TOP
Display the running processes of a container  
`docker container top container-name`

## EXEC
exec will run a command in a running container
`docker container exec -d ubuntu_bash touch /tmp/execWorks`

## Attaching and Detaching

attaching to the container allows you to interact with primary process launched with container eg. python flask voiting app.
`docker container attach CONTAINER_NAME`

to detach `^p ^p`

## INSPECT

`docker container inspect CONTAINER_NAME`

## container stats (cpu memory etc)
`docker container stats`
`docker container stats --no-steam=true`

--

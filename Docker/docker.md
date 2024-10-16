### Basic Commands in Docker

*Always mention image name at the last*

- docker pull <imagename>:<version> will pull the image from hub
- docker ps will list all the running containers
- docker run <imagename>:<version> will start the container, if the image does not exist in the local then
    it will pull from hub and   start
- docker run <imagename> -d this -d will start the container in detached mode so the command prompt is available for next
     commands    to         run 
- docker stop <container id>

- docker start <container id>

- docker ps -a  this -a will list all container running and stopped containers
- docker run <imagename> -p<laptopportnumber>:<containerportnumber>  used to map laptop and container ports
- docker images command will list all available images 
- docker logs <containerid> will give us all the logs
- docker run <imagename> --name <name to be used>
- docker exec -it <containerid/name> 
- docker rm  <containerId/Name> to remove the container
- dcoker ps -aq  will give us all the container ids
-   --no-trunc command will not truncate the container ids

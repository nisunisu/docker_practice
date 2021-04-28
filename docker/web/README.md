```shell
# Create Image
image_name="my_nginx"
docker build -t ${image_name} ./

# Get Images
docker images

# Create Container
image_name="my_nginx"
container_name="my_container"
docker run --name ${container_name} -d -p 8080:80 ${image_name}

# Exec
docker ps
docker exec -it ${container_id} /bin/bash

# Terminate
docker stop ${container_id}
docker rm ${container_id}
docker rmi ${image_name}
```
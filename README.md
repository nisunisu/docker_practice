# my first docker
```zsh
# Create
docker run --name ${container_name} -d -p 8080:80 nginx
docker ps

# attach
docker exec -it ${container_id} /bin/bash

# Terminate
docker stop ${container_id}
docker rm ${container_id}

# Delete image
docker images
docker rmi ${image_name}
```
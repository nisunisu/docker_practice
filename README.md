# Docker compose
1. Prepaere Dockerfile
1. Create image (**When Dockerfile is changed, must do this procedure**)
    ```zsh
    docker compose build --no-cache    
    ```
1. Create a specific container and exec it
    ```zsh
    # service name is specified in docker-compose.yml
    docker compose run ${compose_service_name} bash
    ```
1. Create the set of containers and run it
    ```zsh
    # Up
    docker compose up
    docker compose up -d # runs in background

    # If nginx service does not run correctly, try some of them
    #   1. Use `--forece-recreate` option
    #   1. Change service name in `docker-compose.yml`
    docker compose up --force-recreate
    ```
1. Launch your browser and access to `http://localhost:8080`


# Simple docker sample
```zsh
# Create
docker run --name ${container_name} -d -p 8080:80 nginx
docker ps

# attach
docker exec -it ${container_id} /bin/bash

# Terminate
docker stop ${container_id}
docker rm ${container_id}
docker container prune # Remove all containers

# Delete image
docker images
docker rmi ${image_name}
```
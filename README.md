# Docker compose
1. Prepaere Dockerfile
1. Run `docker compose`
    ```zsh
    # Launch specific container and exec
    # service name is specified in docker-compose.yml
    docker compose run ${compose_service_name} bash

    # Run
    docker compose up
    docker compose up -d # background

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
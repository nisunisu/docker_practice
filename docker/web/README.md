# Prerequisite
1. If you use Docker Hub, set environment variable `USERNAME_DOCKER_HUB`
    ```shell
    export USERNAME_DOCKER_HUB="username/" # "/" is necessary for tag name
    env | grep "USERNAME_DOCKER_HUB"
    ```

# Procedures
1. Create Image
    ```shell
    tag_name=${USERNAME_DOCKER_HUB}"my_nginx"
    docker build -t ${tag_name} ./
    docker images
    ```
1. Create container and exec
    ```shell
    container_name="my_container"
    docker run --name ${container_name} -d -p 8080:80 ${tag_name}
    docker ps
    docker exec -it ${container_id} /bin/bash
    ```
1. Optional : Push image
    ```shell
    docker push ${tag_name}
    ```
1. Remove container
    ```shell
    docker stop ${container_id}
    docker rm ${container_id}
    docker rmi ${tag_name}
    ```

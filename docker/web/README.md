# Dockerfile
## Prerequisite
1. If you use Docker Hub, set environment variable `USERNAME_DOCKER_HUB`
    ```shell
    export USERNAME_DOCKER_HUB="username/" # "/" is necessary for tag name
    env | grep "USERNAME_DOCKER_HUB"
    ```

## Procedures
1. Create Image
    ```shell
    tag_name=${USERNAME_DOCKER_HUB}"my_nginx"
    docker build -t ${tag_name} ./
    docker images
    docker tag ${tag_name} ${some_new_tag_name} # if necessary
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

# Register my docker images to AWS ECR
## Prerequisite
1. Create docker image (See : [Dockerfile](#dockerfile))

## Procedures
1. Set env
    ```shell
    aws_ecr_repo_name="hello-repository"
    region="ap-northeast-1"
    tag_name="hoge" # The tag you upload to ECR. Select from `docker images`
    ```
1. Create ECR repository
    ```shell
    aws ecr create-repository --repository-name ${aws_ecr_repo_name} --region ${region}
    ```
1. Tag image with ECR repository URI
    ```shell
    aws_repo_uri=$(
        aws ecr describe-repositories --repository-names ${aws_ecr_repo_name} | jq -r '.repositories[].repositoryUri'
    )
    docker tag ${tag_name} ${aws_repo_uri}
    ```
1. Login to ECR
    ```shell
    # Get URL from URI.
    aws_repo_url=${aws_repo_uri%%/*} # Remove "/*" by parameter expantion
    
    # Remove current login info
    docker logout
    
    # Set ECR login info
    aws ecr get-login-password | docker login --username AWS --password-stdin ${aws_repo_url} # Username doesn't need to change from "AWS"
    ```
1. Push images to ECR
    ```shell
    ecr_tag_name="latest" # Change as you like
    docker push "${aws_repo_uri}:${ecr_tag_name}"
    
    # Check
    aws ecr describe-images --repository-name ${aws_ecr_repo_name}
    ```
1. Pull images from ECR to local
    ```shell
    docker pull "${aws_repo_uri}:${ecr_tag_name}"
    ```
1. Remove ECR repository
    ```shell
    aws ecr delete-repository --repository-name ${aws_ecr_repo_name} --region ${region} --force
    ```
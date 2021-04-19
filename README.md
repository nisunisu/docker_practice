# my first docker
```zsh
docker run --name hogehoge -d -p 8080:80 nginx
docker ps
docker stop ${container_id}
docker rm ${container_id}
```
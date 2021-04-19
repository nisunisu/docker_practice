# my first docker
```zsh
docker run --name hogehoge -d -p 8080:80 nginx
docker ps

# attach
docker exec -it ${container_id} /bin/bash

docker stop ${container_id}
docker rm ${container_id}
```
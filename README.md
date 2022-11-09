# 启动
docker-compose up

# 进入其中一个容器
docker exec -it redis-1 bash

# 连接集群
redis-cli -c -h [ip] -p [port] -a [pwd]
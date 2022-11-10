# 启动
docker-compose up

# 进入其中一个容器
docker exec -it redis-1 bash

# 连接集群
redis-cli -c -h [ip] -p [port] -a [pwd]

# 查看集群信息
cluster info

# 查看节点信息
cluster nodes
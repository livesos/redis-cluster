# 启动
```shell
docker-compose up
```

# 进入其中一个容器
```shell
docker exec -it redis-1 bash
```
# 开启集群
```shell
redis-cli --cluster create \
192.168.1.3:6381 \
192.168.1.3:6382 \
192.168.1.3:6383 \
192.168.1.3:6384 \
192.168.1.3:6385 \
192.168.1.3:6386 \
--cluster-replicas 1 -a 123456
```

# 连接集群
redis-cli -c -h [ip] -p [port] -a [pwd]

# 集群相关命令
## 集群信息

打印集群信息
```shell
cluster info
```

列出集群当前已知的所有节点,以及这些节点相关的信息
```shell
cluster nodes
```
## 节点

将 ip 和 port 所指定的节点添加到集群当中，让它成为集群的一份子。
```shell
cluster meet <ip> <port>
```

从集群中移除 node_id 指定的节点
```shell
cluster forget <node_id>
```

将当前从节点设置为 node_id 指定的master节点的slave节点。只能针对slave节点操作。
```shell
cluster replicate <master_node_id>
```

将节点的配置文件保存到硬盘里面。
```shell
cluster saveconfig
```

## 槽
将一个或多个槽（ slot）指派（ assign）给当前节点。
```shell
cluster addslots <slot> [slot ...]
```

移除一个或多个槽对当前节点的指派。
```shell
cluster delslots <slot> [slot ...]
```

移除指派给当前节点的所有槽，让当前节点变成一个没有指派任何槽的节点
```shell
cluster flushslots
```

将槽 slot 指派给 node_id 指定的节点，如果槽已经指派给另一个节点，那么先让另一个节点删除该槽>，然后再进行指派
```shell
cluster setslot <slot> node <node_id>
```

将本节点的槽 slot 迁移到 node_id 指定的节点中
```shell
cluster setslot <slot> migrating <node_id>
```

从 node_id 指定的节点中导入槽 slot 到本节点。
```shell
cluster setslot <slot> importing <node_id>
```

取消对槽 slot 的导入（ import）或者迁移（ migrate）
```shell
cluster setslot <slot> stable
```

## 键
计算键 key 应该被放置在哪个槽上。
```shell
cluster keyslot <key>
```
返回槽 slot 目前包含的键值对数量。
```shell
cluster countkeysinslot <slot>
```
返回 count 个 slot 槽中的键
```shell
cluster getkeysinslot <slot> <count> 
```
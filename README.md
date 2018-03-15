# redis-sentinel-docker

使用Docker Compose部署Sentinel模式的Redis集群。

## 使用方法

1. 拉取源码
2. 修改 `docker-compose.yml` 中的 `MASTER_IP` 和 `MASTER_PORT` 参数，以及 `slave_1` 和 `slave_2` 中的Master节点的IP，端口可根据情况修改
3. 修改 `sentinel/sentinel.conf` 中mymaster的IP和端口，和步骤2中修改的保持一致
4. 执行 `docker-compose build --no-cache`
5. 执行 `docker-compose up --scale sentinel=3 -d`

## 运行状态

启动之后，执行`docker-compose ps`，输出：

```
             Name                           Command               State                 Ports              
-----------------------------------------------------------------------------------------------------------
redissentineldocker_master_1     docker-entrypoint.sh redis ...   Up                                       
redissentineldocker_sentinel_1   sentinel-entrypoint.sh           Up      0.0.0.0:1072->26379/tcp, 6379/tcp
redissentineldocker_sentinel_2   sentinel-entrypoint.sh           Up      0.0.0.0:1073->26379/tcp, 6379/tcp
redissentineldocker_sentinel_3   sentinel-entrypoint.sh           Up      0.0.0.0:1071->26379/tcp, 6379/tcp
redissentineldocker_slave_1_1    docker-entrypoint.sh redis ...   Up                                       
redissentineldocker_slave_2_1    docker-entrypoint.sh redis ...   Up                                       
```

可以看到启动了3个Sentinel节点，1个Master节点，2个Slave节点，Sentinel的端口通过bridge网络模式映射到了宿主机的随机端口上，而Master和Slave节点则是使用了host网络模式，解决了其他应用连接不上的问题。

## 参考

[redis-cluster](https://github.com/yunclean/redis-cluster)
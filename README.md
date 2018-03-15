# redis-sentinel-docker

使用Docker Compose部署Sentinel模式的Reids集群。

使用方法：

1. 拉取源码；
2. 修改 `docker-compose.yml` 中的 `MASTER_IP` 和 `MASTER_PORT` 参数，以及 `slave_1` 和 `slave_2` 中的IP，端口可根据情况修改；
3. 执行 `docker-compose build --no-cache`；
4. 执行 `docker-compose up --scale sentinel=3 -d`；


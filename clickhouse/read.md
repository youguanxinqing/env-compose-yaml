# 说明

clickhouse 集群搭建。

# 使用

1. 映射 数据、配置、日志目录:
```bash
# 运行临时容器
$ docker run --name ch-server-tmp --rm yandex/clickhouse-server

# 拷贝配置: ch01, ch02, ch03, ch04
$ docker cp `docker ps | grep ch-server-tmp | awk '{print $1}'`:/etc/clickhouse-server ./ch01/conf/
$ docker cp `docker ps | grep ch-server-tmp | awk '{print $1}'`:/etc/clickhouse-server ./ch02/conf/
$ docker cp `docker ps | grep ch-server-tmp | awk '{print $1}'`:/etc/clickhouse-server ./ch03/conf/
$ docker cp `docker ps | grep ch-server-tmp | awk '{print $1}'`:/etc/clickhouse-server ./ch04/conf/

# 修改用户组
$ chown 101:101 -R ch01
$ chown 101:101 -R ch02
$ chown 101:101 -R ch03
$ chown 101:101 -R ch04

# zk 权限
$ chmod 777 zk -R
```

2. 启动：
```bash
$ docker-compose up
```

3. 连接客户端：
```bash
$ docker run -it --net=clickhouse-net --rm linture/clickhouse-cli -h ch01 # /ch02/ch03/ch04 
```

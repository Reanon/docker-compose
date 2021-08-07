# Docker搭建Zookeeper集群

该脚本使用的

`zookeeper`镜像为：**wurstmeister/zookeeper**



1、安装 `docker-compose`

```shell
# 获取脚本
$ curl -L https://github.com/docker/compose/releases/download/1.25.0-rc2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
# 赋予执行权限
$ chmod +x /usr/local/bin/docker-compose
```

2、下载当前`docker-compose.yml`

```shell
wget https://raw.githubusercontent.com/Reanon/docker-compose/main/zookeeper/docker-compose.yml
```

3、新建 Docker 网络

```shell
# 创建网络
$ docker network create --driver bridge \
    --subnet 172.69.0.0/25 \
    --gateway 172.69.0.1 \
    kafka_zoo
```

4、执行命令 `docker-compose up -d`
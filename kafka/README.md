# Docker 搭建 Kafka集群

⭕️ 使用本脚本之前，请先安装`Zookeeper` 集群

该脚本使用的

> 修改了端口号；在使用过程中出现了只能连接上一个节点的问题。

`Kafka`镜像为：**wurstmeister/kafka**

`Kafka-manager`镜像为：**sheepkiller/kafka-manager**

1、安装 `docker-compose`

```shell
# 获取脚本
# curl 是一种命令行工具，作用是发出网络请求，然后获取数据
curl -L https://github.com/docker/compose/releases/download/1.29.2/run.sh > /usr/local/bin/docker-compose

# 赋予执行权限
# chmod(change mode) 命令是控制用户对文件的权限的命令
chmod +x /usr/local/bin/docker-compose

# 查看版本
docker-compose --version
```

2、下载当前`docker-compose.yml`

```

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


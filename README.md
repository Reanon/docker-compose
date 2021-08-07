# docker-compose
Zookeeper 集群 & Kafka集群 &KafkaManager的docker-compose.yml文件

具体使用方式请参考相应文件夹下具体步骤；

### 集群规划

#### 集群规划

网络名：kafka_zoo 

|   hostname    |     ip      |   port    |
| :-----------: | :---------: | :-------: |
|      zk1      | 172.69.0.21 | 2181:2181 |
|      zk2      | 172.69.0.22 | 2182:2181 |
|      zk2      | 172.69.0.23 | 2183:2181 |
|    kafka1     | 172.69.0.11 | 9091:9091 |
|    kafka2     | 172.69.0.12 | 9092:9092 |
|    kafka3     | 172.69.0.13 | 9093:9093 |
| kafka-manager | 172.69.0.10 | 9002:9000 |

宿主机：xxx.xxx.xxx.xxx

### 准备工作

#### 容器镜像

Zookeeper 镜像：wurstmeister/zookeeper

Kakfa镜像：wurstmeister/kafka

Kafka-Manager镜像：sheepkiller/kafka-manager

#### 安装 docker - compose

```shell
# 获取脚本
# curl 是一种命令行工具，作用是发出网络请求，然后获取数据
curl -L https://github.com/docker/compose/releases/download/1.29.2/run.sh > /usr/local/bin/docker-compose

# 赋予执行权限
# chmod(change mode) 命令是控制用户对文件的权限的命令
chmod +x /usr/local/bin/docker-compose
```

#### 创建集群网络

基于 Linux 宿主机而工作的，也是在 Linux 宿主机创建，创建之后 Docker 容器中的各个应用程序可以使用该网络。

```shell
# 创建网络
$ docker network create --driver bridge \
    --subnet 172.69.0.0/25 \
    --gateway 172.69.0.1 \
    kafka_zoo
```

通过`docker network ls`可以查看到网络类型中多了一个 zookeeper-kafka

```shell
# 查看 docker 网络
docker network ls
```





### 集群搭建

> Tips：应先创建 Docker 网络（参考相应文件夹下的README.md）
>
> 再安装`Zookeeper`，最后安装`Kafka`和`KafkaManager`；

#### Zookeeper 集群

`zookeeper`镜像为：wurstmeister/zookeeper

运行命令

```shell
docker-compose -f ./zookeeper/docker-compose.yml up -d

docker-compose -f ./kafka/docker-compose.yml up -d
```


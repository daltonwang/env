# 使用Docker安装Redis

###  1.  拉取redis官方镜像

```
docker pull redis
```
- 如果无法下拉，请使用国内镜像

具体方法， 在/etc/docker/目录下创建 daemon.json，并在内增加如下部分：

```
{
        "registry-mirrors": ["https://registry.docker-cn.com","https://pee6w651.mirror.aliyuncs.com"]
}
```




### 2. 查看镜像
```
docker images
```
### 3. 启动redis

#### 3.1 简易启动方式

```
docker run -it -p 6379:6379 --name myredis docker.io/redis
```

#### 3.2 脚本启动方式

##### 3.2.1 设置配置文件

redis.conf 从github中下载，注意其中

##### 3.2.2 设置文件挂载目录

在容器的宿主机上创建两个用于挂载文件的目录

/opt/docker/redis/conf

/opt/docker/redis/data

将redis.conf拷贝到/opt/docker/redis/conf中

##### 3.2.3 启动脚本

启动脚本的核心命令：

    docker run -p 6379:6379 \
        --privileged=true \
        --name redis \
        --volume /docker/redis/conf/redis.conf:/etc/redis/redis.conf \
        --volume /docker/redis/data:/data \
        --volume /etc/localtime:/etc/localtime \
        --restart=unless-stopped \
        docker.io/redis \
        redis-server /etc/redis/redis.conf --appendonly yes 


### 4. 查看redis服务

```
docker ps
```
### 5. 测试
```
docker exec -it [容器id] redis-cli
```



## 常见FAQ

1. ##### 如何查看Redis日志？

2. 
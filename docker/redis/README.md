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

- 简易启动方式

```
docker run -it -p 6379:6379 --name myredis docker.io/redis
```

- 脚本启动方式，利用系统提供的start_redis.sh文件进行启动

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
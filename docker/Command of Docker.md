### Docker 常用命令
#### 帮助命令
1. 查看docker版本

```
docker version
```
2. 查看docker信息

```
docker info
```
3. 查看docker命令
```
docker --help
```
#### 镜像命令
1. 列出本地镜像
```
docker images
docker images -a #列出本地所有的镜像
docker images -q #只显示ID
docker images -qa #列出所有的镜像ID
docker images --digests #显示镜像的摘要信息
docker images --no-trunc #显示完整的镜像信息
```

2. 从 https://hub.docker.com 查找镜像
```
docker images search (image name)
docker images search (-s 50 image name) #查找星数大于50的指定镜像
docker images search (-s 50 --no-trunc image name) #查找星数大于50的指定镜像的详细信息
```
3. 下载镜像
```
docker pull (image name[: TAG])
```
4. 删除某个镜像
```
docker rmi (image name[: TAG])
docker rmi -f (image name[: TAG])  强制删除
docker rmi -f $(docker images -qa) 全部删除
```
5. Dockerfile构建docker镜像

```
docker build -f Dockerfile -t imageName .
```
6. Docker重命名镜像REPOSITORY和TAG
```
docker tag IMAGEID(镜像id) REPOSITORY:TAG
```

#### 容器命令
1. 新建并启动容器
```
docker run [OPTIONS] IMAGE [COMMAND] [ARGS...]

                    OPTIONS:
                                     --name="容器名称"：为容器指定一个名称
                                     -d：后台运行容器，并返回容器ID，即启动守护式容器
                                     -i：以交互模式运行容器，通常与-t同时使用
                                     -t：为容器重新分配一个伪输入终端，通常与-i同时使用
                                     -P：随机端口映射
                                     -p：指定端口映射，有以下四种格式：
                                             ip:hostPort:containerPort
                                             ip::containerPort
                                             hostPort:containerPort
                                             containerPort
                                     （例：docker run -it -p 8888:8080 tomcat         
                                        docker启动tomcat容器，8888为docker端口、8080为tomcat容器的端口，访问路径为docker端口，即IP:8888）
                    注：Docker容器后台运行就必须要有一个前台进程，容器运行命令如果不是一直挂起的命令（如：top,taail），会自动退出。
                           (docker run -d centos /bin/sh -c "while true; do echo hello; sleep 2;done"，后台启动容器并持续交互)
```
2. 列出当前所有正在运行的容器
```
        docker ps [OPTIONS]

                    OPTIONS:

                                     -a：列出当前所有正在运行的容器和历史运行过的容器

                                     -l：显示最近创建的容器

                                     -n args：显示最近n个创建的容器

                                     -q：静默模式，只显示容器编号

                                     --no-trunc：不截断输出
```
3. 退出容器
```
        exit：容器停止退出

        ctrl+P+Q：容器不停止退出
```
4. 启动容器
```
        docker start containerID | containerName
```
5. 重启容器
```
        docker restart containerID | containerName
```
6. 停止容器
```
        docker stop containerID | containerName
```
7. 强制停止容器
```
        docker kill containerID | containerName
```
8. 删除已停止容器
```
        docker rm containerID
```
9. 查看容器日志
```
        docker logs -f -t --tail containerID

                    -t：加入时间戳

                    -f：跟随最新日志打印

                    -tail：数字 显示最后多少条
```
10. 查看容器内运行的进程
```
        docker top containerID
```
11. 查看容器内部细节
```
        docker inspect containerID
```
12. 进入正在运行的容器并以命令行交互
```
        docker attach containerID                           直接进入容器命令终端，不会启动新的进程

        docker exec -t containerID (/bin/bash)        在容器中打开新的终端，并且可以启动新的进程
```
13. 从容器内拷贝文件到宿主机
```
        docker cp containerID:容器内的路径 宿主机路径
```
14. 提交容器副本使之成为新的镜像
```
        docker commit -a="author" -m="desc" containerID imageRepository
```
#### Docker常用启动命令
启动Tomcat：
```
docker run -d -p 8888:8080 --name containerName -v /mnt/docker/tomcat/dataVolumes/test:/usr/local/apache-tomcat-9.0.10/webapps/test -v /mnt/docker/tomcat/dataVolumes/logs:/usr/local/apache-tomcat-9.0.10/logs --privileged=true imageName
```
启动MySQL：
```
docker run -p 8761:3306 --name mysql5.6 -v /mnt/docker/mysql/conf:/etc/mysql/conf.d -v /mnt/docker/mysql/logs:/logs -v /mnt/docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:5.6 
```
备份MySQL数据：
```
docker exec containerID sh -c ' exec mysqldump --all-databases -uroot -p"root"' > /mnt/docker/mysql/data/databases.sql
```
启动Redis：
```
docker run -p 6379:6379 --name redisServer -v /mnt/docker/redis/data:/data -v /mnt/docker/redis/conf/redis.conf:/usr/local/etc/redis/redis.conf -d redis:3.2 redis-server /usr/local/etc/redis/redis.conf --appendonly yes
```
启动Nginx：
```
docker run --name myNginx -it -p 8088:80 -v /mnt/docker/nginx/html:/usr/share/nginx/html -v /mnt/docker/nginx/conf/nginx.conf:/etc/nginx/nginx.conf:ro -v /mnt/docker/nginx/conf.d:/etc/nginx/conf.d nginx:latest
```
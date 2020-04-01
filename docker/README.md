# CentOS上安装Docker

centos 官方提供版本社区版安装

```
yum install docker
```

查看docker版本

```
docker version
```

docker启动:

```
systemctl start docker
```


将docker作为系统进程：

```
systemctl enable docker
```

查看docker进程

```
ps -ef|grep docker
```



参考文献：

- https://blog.csdn.net/u011943534/article/details/81252894
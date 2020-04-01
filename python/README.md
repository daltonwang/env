# Centos环境下的Python安装

### 安装Python3

先用whereis查看系统里是否已经安装python

```
whereis python
```
如果系统里没有Python3， 则可以进行安装。

```
yum install python3
```

注意CentOS自带Python2.7， 如果安装完Python3之后，内部会存在多个Python的版本，具体的对应情况需要到/usr/bin下查看。 一般情况下，默认的python还是python2, 如果需要python3.7，需要输入Python3。

如果想把python3做成默认Pothon，则需要建立软链接。到/usr/bin下操作
```
rm python
ln -s python3 python
```

需要注意python安装对yum的影响，因为Yum是采用python2的，如果Python做了软链接，则需要修改yum的配置
```
vi /usr/bin/yum
把#! /usr/bin/python修改为#! /usr/bin/python2

vi /usr/libexec/urlgrabber-ext-down
把#! /usr/bin/python 修改为#! /usr/bin/python2
```
### 安装pip

首先安装EPEL源
```
yum -y install epel-release  
```
然后安装pip
```
yum -y install python-pip   
```
注意pip安装之后，存在pip, pip2, pip3多种版本。 要注意区分使用。可以通过下面命令查看pip的版本

```
pip --version  查看pip版本
pip2 -V
pip3 -V
```

更换pip国内源
```
cd ~
mkdir .pip
cd .pip
vi ~/.pip/pip.conf
[global]
trusted-host =  mirrors.aliyun.com
index-url = https://mirrors.aliyun.com/pypi/simple
```
如果需要更新pip
```
pip2 install --upgrade pip
pip3 install --upgrade pip
```

###  安装EPEL 阿里镜像源

官方EPEL源的数据可能会比较慢，可以换成阿里的镜像源。首先备份(如有配置其他epel源) 

```
mv /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel.repo.backup
mv /etc/yum.repos.d/epel-testing.repo /etc/yum.repos.d/epel-testing.repo.backup
```

下载阿里镜像源的配置文件

```
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
```

运行生成缓存
```
yum makecache
```
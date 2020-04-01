# VMWARE 环境设置向导



## 一、 VMWare安装

注意事项：需要释放鼠标的时候按 Ctrl+Alt

## 二、 镜像下载

#### 2.1 CentOS

##### 2.1.1 版本选择

- 目前一般选择7.6

##### 2.1.2 镜像下载地址：

- 官方ISO版本： https://www.centos.org/ 

- 国内的阿里镜像源 http://mirrors.aliyun.com/centos/
- 对应的镜像文件可以下载：http://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1908.iso

 #### 2.2  Ubuntu

##### 2.2.1 版本选择

- 目前一般选择18.04

##### 2.2.2 镜像下载地址：

- 官方ISO版本：https://ubuntu.com/download/server 。 我在试用ubuntu安装的时候有问题，后来一直没有使用这个镜像。

## 三、 CentOS基础虚拟机安装

1. 选择Centos Mini镜像进行安装；

2. 选择2 Core, 4G进行内存配置；

3. 网络适配器选择“仅主机模式”；

4. 按照提示一步步进行，到网络部分，将网络配置打开，将网络地址配置为“192.168.137.100”（C类地址和vnet0保持一致，最后一位按照自己喜好定义），注意网关地址也要进行配置。如果有需要，再配置一下HOST name;

5. 设置一个root密码供自己使用；

四、 CentOS基础虚拟机环境配置

## 四、CentOS基础环境配置

#### 4.1 网卡
##### 修改静态地址配置
在/etc/sysconfig/network-scripts/找到对应的网卡配置文件，把网卡配置改成静态配置
```
BOOTPROTO="static"
```
##### 域名解析
在/etc/sysconfig/network-scripts/找到对应的网卡配置文件，增加域名解析服务器地址：

```
DNS1=8.8.8.8
DNS2=114.114.114.114
```

编辑 /etc/resolv.conf，增加域名解析服务器
```
nameserver 8.8.8.8
nameserver 114.114.114.114
```
其他常用的域名解析服务器还有：
114.114.114.114
114.114.115.115
223.5.5.5 阿里
223.6.6.6 阿里
180.76.76.76 百度

注意网络配置之后要重启机器。 重启之后 ping www.baidu.com.cn ， 检查看是否正常。

#### 4.2 启动菜单时间

```shell
vi /etc/grub2/grub.cfg
```

搜索timeout=5, 将值修改成0

#### 4.3 关闭SELinux
- 临时关闭
```
setenforce 0                  ##设置SELinux 成为permissive模式
```


- 永久关闭– 需要重启服务器
```shell
修改/etc/selinux/config文件中设置SELINUX=disabled ，然后重启服务器。
```

#### 4.4 关闭firewalld
停止和禁用firewalld
```
systemctl disable firewalld
systemctl stop firewalld
```

#### 4.5 修改163 repo 源
首先备份/etc/yum.repos.d/CentOS-Base.repo。 此时如果没有安装wget, 可以先安装wget或者使用curl

```shell
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
mv CentOS7-Base-163.repo CentOS-Base.repo
yum clean all
yum makecache
yum update
```



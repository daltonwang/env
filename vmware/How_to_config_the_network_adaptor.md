## 环境

https://blog.csdn.net/xiehd313/article/details/80814584
#### Workstation上的网络模式
##### VMWARE虚拟机网络配置
- 点击菜单上的“编辑”
- 选择“虚拟网络编辑器” ，配置vmnet1和vmnet8的网络配置
- vmnet1是主机模式，这里需要将该模式的DHCP和掩码配置好（192.168.200.0, 255.255.255.0）
- vmnet8是NAT模式，这里需要将该模式的DHCP和掩码配置好（192.168.100.0, 255.255.255.0）

##### 虚拟机模式选择
- 右击打开的虚拟机， 选择“设置”
- 点击“网络适配器”， 选择“NAT”模式

##### 虚拟机网卡配置
- 进入centos系统

```
vi /etc/sysconfig/network-scripts/ifcfg-ens33

```
- 编辑该文件ifcfg-ens33（不同网卡文件不同）


```
ONBOOT=yes
DNS1=114.114.114.114
DNS2=8.8.8.8
ZONE=public
```
- 如果需要指定IP地址，则需要修改
```
BOOTPROTO=static
IPADDR=192.168.100.100
NETMASK=255.255.255.0
GATEWAY=192.168.100.2
```

- 重新启动
```
systemctl restart network.service
```



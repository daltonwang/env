#### CentOS 7.6 上 SSH免秘钥登录
##### 环境
- CentOS
- XShell 5.x
##### 步骤
###### 生成公私钥对
1. 利用XShell的用户秘钥管理工具，选择算法和位数生成；
2. 将公钥文件保存为.pub文件
###### CentOS配置
- 打开/etc/sshd/
- vi /etc/sshd/ssh_config, 修改：PubkeyAuthentication yes
- 打开 ~/.SSh/
- 将公钥复制到该目录，并修改成authorized_keys （该名称是配置文件中配置）
- chmod 600 authorized_keys
###### XShell配置
- 选择公钥登录
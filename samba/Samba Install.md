https://blog.csdn.net/fakine/article/details/91351393

### Disable Firewall
'''
systemctl stop firewalld.service 
systemctl disable firewalld.service 
'''

### Disable SELINUX
'''
cat /etc/selinux/config 

SELINUX=disabled
SELINUXTYPE=targeted
'''


### Installtion
'''
#install
yum install samba

#check
rpm -qa | grep samba
'''

### Configuration
'''
    #======================= Global Settings =====================================
     
    [global]                                                  
    # ----------------------- Network Related Options -------------------------
    #
    # workgroup = NT-Domain-Name or Workgroup-Name, eg: MIDEARTH
    #
    # server string is the equivalent of the NT Description field
    #
    # netbios name can be used to specify a server name not tied to the hostname
     
    workgroup = WORKGROUP                             
    server string = Liuyunsheng Samba Server Version %v     
    netbios name = Liuyunsheng-Samba                         
    # --------------------------- Logging Options -----------------------------
    #
    # Log File let you specify where to put logs and how to split them up.
     
    log file = /var/log/samba/log.%m                  
                                                              
    # ----------------------- Standalone Server Options ------------------------
    #
    # Scurity can be set to user, share(deprecated) or server(deprecated)
     
    security = user 
    map to guest = Bad User                                 
    #============================ Share Definitions ==============================
     
    [public]                                          
    comment = Public Stuff                            
    path = /home/test/test
    writeable = yes
    public = yes 
'''

### Start Samba Service
'''
systemctl start smb
systemctl status smb
'''

### Create Account
1. Create Linux Account
'''
gourpadd test -g 6000
useradd test -u 6000 -g 6000 -s /sbin/nologin -d /dev/null
'''

2. Create Samba Account
'''
smbpasswd -a test
'''

### Delete Account
'''
smbpasswd -x test
'''


### How to accecss it from windows
- 在windows中输入 \\192.168.0.1\


### 	Q&A
##### 采用window打开共享目录后，无法写入文件
可能性有三种
1. 在smb.conf没有配置writeable
2. 原始目录没有权限，需要chmod 766 或者666
3. SELINUX的阻挡

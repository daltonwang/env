### git usage
- git status
- git checkout xxxx  //checkout branch 
- git add
- git commit -m "comment for commit"
- git push

### github usage
#### github ssh
- Generate SSH Key
```
    $ ssh-keygen -t rsa -C "your_email@example.com"
        代码参数含义：
        -t 指定密钥类型，默认是 rsa ，可以省略，还可以指定为 dsa。
        -C 设置注释文字，比如邮箱。
        -f 指定密钥文件存储文件名。可以省略，使用默认值 id_rsa 和 id_rsa.pub
```
- 在/root/.ssh下会生成 “id_rsa”、“id_rsa.pub”
- 将pub作为ssh 添加到github中去。


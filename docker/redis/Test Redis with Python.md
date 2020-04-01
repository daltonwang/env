# 使用Python测试Redis

### 安装redis支持包

```
 pip3 install redis
```


### 使用python测试Redis
在终端下输入命令 python进入python的控制终端，首先导入redis支持包。
```
>>import redis
>>#连接redis 这个方法是从连接池中取出一个连接并返回
>>Conn = redis.StrictRedis(host='localhost',port='6379',db='0')
>>#连接成功后便可使用Conn操作数据库
>>Conn.set('helloworld','hello,Im python')
>>Conn.get('helloworld')
```
那么使用连接池连接
```
>>pool = redis.ConnectionPool(host='localhost',port='6379',db=0)
>>conn = redis.Redis(connection_pool=pool)
```


### 安装pip工具
```
sudo apt install python-pip
```

### 如果报错locale的错误
```
export LC_ALL=en_US.UTF-8
``` 
### 安装shadowsocks
```
sudo pip install shadowsocks
```

### 编辑配置文件
```
sudo vim /etc/shadowsocks.json
{
    "server":"0.0.0.0",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"moma135",
    "timeout":300,
    "method":"aes-256-cfb"
}

sudo chmod 755 /etc/shadowsocks.json
```

### 启动服务
```
sudo ssserver -c /etc/shadowsocks.json -d start
sudo ssserver -c /etc/shadowsocks.json -d stop
```

### 添加开机自启动
```
sudo vim /etc/rc.local中添加
ssserver -c /etc/shadowsocks.json -d start
```

[启动报错参考](https://blog.csdn.net/blackfrog_unique/article/details/60320737)

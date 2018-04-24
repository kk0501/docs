##  源码安装教程
[官网地址](https://docs.gitlab.com/ce/install/installation.html)

## ubuntu16.04上gitlab安装教程
### 安装依赖
```
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates
```

### 安装邮件系统， 用来发送通知
```
sudo apt-get install -y postfix
```

### 添加gitlab-ce的deb源
```
cd /tmp
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
```

### 安装gitlab
```
sudo EXTERNAL_URL="your host" apt-get install gitlab-ce
```

### 配置
```
sudo vim /etc/gitlab/gitlab.rb
```

### 启动
```
sudo gitlab-ctl reconfigure
```
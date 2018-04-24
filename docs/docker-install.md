## ubuntu16.04 安装docker
### 卸载旧的docker
```
sudo apt-get remove docker docker-engine docker.io
```

### 安装依赖包
```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

### 导入gpg秘钥
```
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

### 添加apt源
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

### 安装docker-ce
```
sudo apt-get update
sudo apt-get install docker-ce
```

### 安装docker-compose
```
sudo curl -L https://github.com/docker/compose/releases/download/1.21.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

### 升级docker-compose
```
docker-compose migrate-to-labels
```
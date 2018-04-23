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
sudo EXTERNAL_URL="http://192.168.1.2" apt-get install gitlab-ce
```

### 配置
```
sudo vim /etc/gitlab/gitlab.rb
```

### 启动
```
sudo gitlab-ctl reconfigure
```

##  源码安装教程
### 安装sudo
```
apt-get update -y
apt-get upgrade -y
apt-get install sudo -y
```

### 安装vim
```
sudo apt-get install -y vim
sudo update-alternatives --set editor /usr/bin/vim.basic
```

### 安装依赖包
```
sudo apt-get install -y build-essential zlib1g-dev libyaml-dev libssl-dev libgdbm-dev libre2-dev libreadline-dev libncurses5-dev libffi-dev curl openssh-server checkinstall libxml2-dev libxslt-dev libcurl4-openssl-dev libicu-dev logrotate rsync python-docutils pkg-config cmake
```

### 安装git
```
sudo apt-get install -y git-core
```

### 安装邮件系统
```
sudo apt-get install -y postfix
```

### 安装ruby

### 安装golang

### 安装nodejs

### create user
```
sudo adduser --disabled-login --gecos 'GitLab' git
```

### 安装数据库
- 安装
```
sudo apt-get install -y postgresql postgresql-client libpq-dev postgresql-contrib
```
- 创建数据库
```
sudo -u postgres psql -d template1 -c "CREATE USER git CREATEDB;"
sudo -u postgres psql -d template1 -c "CREATE EXTENSION IF NOT EXISTS pg_trgm;"
sudo -u postgres psql -d template1 -c "CREATE DATABASE gitlabhq_production OWNER git;"
sudo -u git -H psql -d gitlabhq_production
```
- 检测
```
SELECT true AS enabled
FROM pg_available_extensions
WHERE name = 'pg_trgm'
AND installed_version IS NOT NULL;
```

### 安装redis
```
sudo apt-get install redis-server
sudo usermod -aG redis git
```

### 下载源码
```
sudo -u git -H git clone https://gitlab.com/gitlab-org/gitlab-ce.git -b 10-7-stable gitlab
```

### 配置
```
# Go to GitLab installation folder
cd /home/git/gitlab

# Copy the example GitLab config
sudo -u git -H cp config/gitlab.yml.example config/gitlab.yml

# Update GitLab config file, follow the directions at top of file
sudo -u git -H editor config/gitlab.yml

# Copy the example secrets file
sudo -u git -H cp config/secrets.yml.example config/secrets.yml
sudo -u git -H chmod 0600 config/secrets.yml

# Make sure GitLab can write to the log/ and tmp/ directories
sudo chown -R git log/
sudo chown -R git tmp/
sudo chmod -R u+rwX,go-w log/
sudo chmod -R u+rwX tmp/

# Make sure GitLab can write to the tmp/pids/ and tmp/sockets/ directories
sudo chmod -R u+rwX tmp/pids/
sudo chmod -R u+rwX tmp/sockets/

# Create the public/uploads/ directory
sudo -u git -H mkdir public/uploads/

# Make sure only the GitLab user has access to the public/uploads/ directory
# now that files in public/uploads are served by gitlab-workhorse
sudo chmod 0700 public/uploads

# Change the permissions of the directory where CI job traces are stored
sudo chmod -R u+rwX builds/

# Change the permissions of the directory where CI artifacts are stored
sudo chmod -R u+rwX shared/artifacts/

# Change the permissions of the directory where GitLab Pages are stored
sudo chmod -R ug+rwX shared/pages/

# Copy the example Unicorn config
sudo -u git -H cp config/unicorn.rb.example config/unicorn.rb

# Find number of cores
nproc

# Enable cluster mode if you expect to have a high load instance
# Set the number of workers to at least the number of cores
# Ex. change amount of workers to 3 for 2GB RAM server
sudo -u git -H editor config/unicorn.rb

# Copy the example Rack attack config
sudo -u git -H cp config/initializers/rack_attack.rb.example config/initializers/rack_attack.rb

# Configure Git global settings for git user
# 'autocrlf' is needed for the web editor
sudo -u git -H git config --global core.autocrlf input

# Disable 'git gc --auto' because GitLab already runs 'git gc' when needed
sudo -u git -H git config --global gc.auto 0

# Enable packfile bitmaps
sudo -u git -H git config --global repack.writeBitmaps true

# Enable push options
sudo -u git -H git config --global receive.advertisePushOptions true

# Configure Redis connection settings
sudo -u git -H cp config/resque.yml.example config/resque.yml

# Change the Redis socket path if you are not using the default Debian / Ubuntu configuration
sudo -u git -H editor config/resque.yml
```

### 配置数据库
```
# PostgreSQL only:
sudo -u git cp config/database.yml.postgresql config/database.yml

# MySQL only:
sudo -u git cp config/database.yml.mysql config/database.yml

# MySQL and remote PostgreSQL only:
# Update username/password in config/database.yml.
# You only need to adapt the production settings (first part).
# If you followed the database guide then please do as follows:
# Change 'secure password' with the value you have given to $password
# You can keep the double quotes around the password
sudo -u git -H editor config/database.yml

# PostgreSQL and MySQL:
# Make config/database.yml readable to git only
sudo -u git -H chmod o-rwx config/database.yml
```


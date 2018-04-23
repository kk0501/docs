## 使用rbenv方式安装ruby
### 安装rbenv
```
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
```

### 安装ruby
```
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
```

### 测试安装
```
rbenv install 2.5.0
rbenv global 2.5.0
ruby -v
```

### 安装bundle
```
gem install bundler
rbenv rehash
```

### 安装rails
```
gem install rails -v 5.1.4
```
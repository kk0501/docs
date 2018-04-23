## ubuntu16.04
### 安装phpunit
```
sudo curl -OL https://phar.phpunit.de/phpunit-7.0.phar
sudo chmod +x phpunit-7.0.phar
sudo mv phpunit-7.0.phar /usr/local/bin/phpunit 
```

### 安装composer
```
curl https://getcomposer.org/installer | sudo php -- 
sudo mv composer.phar /usr/local/bin/composer 
sudo chmod +x /usr/local/bin/composer
```

### 安装php-cs-fixer
```
composer global require friendsofphp/php-cs-fixer
export PATH="$PATH:$HOME/.composer/vendor/bin"
```
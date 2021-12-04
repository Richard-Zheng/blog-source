---
title: 安装和配置 Flarum
date: 2021-12-02 19:45:00 +08:00
tags: 
---

本文采用 Ubuntu 20.04 LTS.

## 安装 MariaDB、PHP 和 Composer

更新源

```
sudo apt update
```

首先安装 php（Apache 2 的 php 模块）

```bash
sudo apt-get install apache2 mariadb-server php7.4 libapache2-mod-php7.4 php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-mysql php7.4-gd php7.4-xml php7.4-curl php7.4-cli php7.4-zip php7.4-tokenizer wget unzip curl git -y
```

然后全局安装 Composer

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

## 配置数据库

运行

```
sudo mysql_secure_installation
```

- Enter current password for root (enter for none): Just press the Enter
- Set root password? [Y/n]: Y
- New password: Enter password
- Re-enter new password: Repeat password
- Remove anonymous users? [Y/n]: Y
- Disallow root login remotely? [Y/n]: Y
- Remove test database and access to it? [Y/n]:  Y
- Reload privilege tables now? [Y/n]:  Y

```
sudo mysql -u root -p
create database flarum character set utf8mb4 collate utf8mb4_unicode_ci;
CREATE USER 'flarumuser'@'localhost' IDENTIFIED BY 'new_password_here';
GRANT ALL ON flarum.* TO 'flarumuser'@'localhost' IDENTIFIED BY 'user_password_here' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```

## 安装 Flarum 并配置 Apache

创建目录并使当前用户成为所有者。这是为了避免以 root 运行 Composer.

```
sudo mkdir -p /var/www/flarum
sudo chown -R $USER:$USER /var/www/flarum
```

安装

```
cd /var/www/flarum
composer create-project flarum/flarum .
```

然后，使 Apache 成为该目录的所有者

```
sudo chown -R www-data:www-data /var/www/flarum
```

添加 Apache 的 VirtualHost

```
sudo vim /etc/apache2/sites-available/flarum.conf
```

写入以下内容

```
<VirtualHost *:80>
    ServerAdmin admin@your_domain.com
    DocumentRoot /var/www/flarum/public
    ServerName your-server
    <Directory /var/www/flarum/public>
        Options FollowSymlinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/your-domain.com_error.log
    CustomLog ${APACHE_LOG_DIR}/your-domain.com_access.log combined
</VirtualHost>
```

启用新的 VirtualHost 和 URL 重写模块，并通过重启服务来应用更改。

```
sudo a2ensite flarum
sudo a2enmod rewrite
sudo a2dissite 000-default.conf
sudo systemctl restart apache2
```

检查是否已打开防火墙。

## 配置 HTTPS

安装 certbot

```
sudo apt install certbot python3-certbot-apache
```

确保 `flarum.conf` 中填入了正确的域名。

允许 SSL 通过防火墙

- 检查云服务提供商的防火墙已打开 443 端口
- 检查 `ufw` 设置 `sudo ufw status`

申请 SSL 证书

```
sudo certbot --apache
```


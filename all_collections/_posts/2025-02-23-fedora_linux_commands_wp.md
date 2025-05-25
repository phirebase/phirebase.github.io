---
layout: post
title: "Essential Fedora Linux Commands for WordPress Developers"
date: 2025-02-23
categories: [development, fedora, wordpress, tools]
---  

## Introduction

For WordPress developers using Fedora Linux, knowing essential Linux commands can significantly improve productivity. This guide covers key commands for managing the system, working with files, setting up development environments, and troubleshooting WordPress-related issues.

## System Management Commands

### Update and Upgrade System

Ensure your system is up to date:

```sh
sudo dnf update -y && sudo dnf upgrade -y
```

### Check System Information

View general system information:

```sh
uname -a
hostnamectl
```

Check available disk space:

```sh
df -h
```

Monitor system resource usage:

```sh
top
htop  # Requires installation: sudo dnf install -y htop
```

## File and Directory Management

### Navigating Directories

```sh
cd /var/www/html  # Move to WordPress installation folder
ls -la            # List files with permissions
pwd               # Print current directory
```

### Creating and Removing Files/Directories

```sh
touch myfile.txt  # Create a new file
mkdir myfolder    # Create a new directory
rm -rf myfolder   # Remove directory and its contents
```

### Editing Files

```sh
nano wp-config.php  # Edit a file with Nano
vim wp-config.php   # Edit a file with Vim
```

## WordPress Development Commands

### Install Required Packages

Install essential PHP, MySQL, and Apache dependencies:

```sh
sudo dnf install -y httpd php php-cli php-mysqlnd php-curl php-json php-xml mariadb-server
```

### Manage Apache and MySQL Services

Start and enable Apache:

```sh
sudo systemctl start httpd
sudo systemctl enable httpd
```

Start and enable MySQL:

```sh
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Secure MySQL installation:

```sh
sudo mysql_secure_installation
```

## WP-CLI Commands

### Install WP-CLI

```sh
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
```

### Manage WordPress Installations

```sh
wp core download
wp core install --url="example.com" --title="My Site" --admin_user="admin" --admin_password="password" --admin_email="admin@example.com"
```

Update WordPress core, themes, and plugins:

```sh
wp core update
wp plugin update --all
wp theme update --all
```

## Docker for WordPress Development

### Install Docker and Docker Compose

```sh
sudo dnf install -y docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
sudo dnf install -y docker-compose
```

### Set Up a WordPress Environment with Docker

```sh
mkdir wordpress-docker && cd wordpress-docker
```

Create `docker-compose.yml`:

```yaml
version: '3.8'
services:
  wordpress:
    image: wordpress:latest
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppassword
      WORDPRESS_DB_NAME: wpdatabase
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: wpdatabase
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppassword
```

Start the containers:

```sh
docker-compose up -d
```

## Debugging and Logs

### Check Apache Logs

```sh
tail -f /var/log/httpd/access_log
```

### Check MySQL Logs

```sh
tail -f /var/log/mariadb/mariadb.log
```

### Debug PHP Errors in WordPress

Enable debugging in `wp-config.php`:

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
@ini_set('display_errors', 0);
```

View debug log:

```sh
tail -f wp-content/debug.log
```

## Conclusion

Mastering these essential Fedora Linux commands can make WordPress development more efficient, whether you are managing files, setting up development environments, or debugging issues. Keep these commands handy to streamline your workflow!

Happy coding! 🚀

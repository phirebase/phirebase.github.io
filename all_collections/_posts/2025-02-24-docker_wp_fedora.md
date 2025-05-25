---
layout: post
title: "Essential Fedora Linux Commands for WordPress Developers"
published: false
date: 2025-02-24
categories: [development, docker, fedora, wordpress, tools]  
---

## Introduction

Using Docker for WordPress development on Fedora provides a lightweight and flexible alternative to LocalWP. With Docker, you can quickly spin up isolated WordPress environments without the need for manual LAMP/LEMP stack configurations.

This guide will walk you through installing Docker on Fedora, setting up a WordPress development environment, and managing your containers efficiently.

## Prerequisites

Ensure you have the following before starting:

- Fedora Linux (any recent version)
- Basic familiarity with Docker and WordPress
- Sudo access

## Step 1: Install Docker on Fedora

Docker is available in Fedora's official repositories. To install it, run:

```sh
sudo dnf install -y dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf install -y docker-ce docker-ce-cli containerd.io
```

Start and enable the Docker service:

```sh
sudo systemctl start docker
sudo systemctl enable docker
```

Verify installation:

```sh
docker --version
```

If you want to run Docker commands without `sudo`, add your user to the `docker` group:

```sh
sudo usermod -aG docker $USER
newgrp docker
```

## Step 2: Install Docker Compose

Docker Compose simplifies managing multi-container applications like WordPress.

```sh
sudo dnf install -y docker-compose
```

Verify installation:

```sh
docker-compose --version
```

## Step 3: Set Up a WordPress Development Environment

Create a new directory for your WordPress project:

```sh
mkdir ~/wordpress-docker && cd ~/wordpress-docker
```

Create a `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress_dev
    restart: always
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppassword
      WORDPRESS_DB_NAME: wpdatabase
    volumes:
      - ./wp-content:/var/www/html/wp-content

  db:
    image: mysql:5.7
    container_name: wordpress_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: wpdatabase
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppassword
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

## Step 4: Start Your WordPress Environment

Run the following command to start your WordPress containers:

```sh
docker-compose up -d
```

Check running containers:

```sh
docker ps
```

Your WordPress site should now be accessible at [http://localhost:8000](http://localhost:8000).

## Step 5: Managing Your Containers

### Stopping Containers

To stop your WordPress setup, run:

```sh
docker-compose down
```

### Restarting Containers

To restart the containers after shutting them down:

```sh
docker-compose up -d
```

### Viewing Logs

To view real-time logs:

```sh
docker-compose logs -f
```

## Step 6: Customizing WordPress

To modify your WordPress files, navigate to the `wp-content` directory in your project folder:

```sh
cd ~/wordpress-docker/wp-content
```

You can add themes and plugins manually or use WP-CLI inside the WordPress container:

```sh
docker exec -it wordpress_dev bash
```

Once inside the container, you can install WP-CLI:

```sh
apt update && apt install -y curl unzip
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x wp-cli.phar
mv wp-cli.phar /usr/local/bin/wp
```

Verify WP-CLI installation:

```sh
wp --info
```

## Conclusion

Docker provides an efficient and reproducible environment for WordPress development on Fedora. With Docker Compose, you can easily manage your WordPress instance and database without complex manual configurations.

Happy coding! 🚀

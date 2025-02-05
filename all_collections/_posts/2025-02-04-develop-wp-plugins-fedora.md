---
layout: post
title: "Developing and Testing WordPress Plugins on Fedora Linux"
date: 2025-02-04
categories: [development, fedora, wordpress, plugins, tools]
---

## Introduction

Developing WordPress plugins on Fedora Linux requires a well-configured development environment. This guide will walk you through setting up everything you need, from installing WordPress locally to testing and debugging your plugins effectively.

## Prerequisites

Before you start, ensure you have the following:

- Fedora Linux (any recent version)
- Basic knowledge of WordPress development
- PHP and MySQL installed
- WP-CLI for managing WordPress via the command line
- A local WordPress environment (LocalWP, LAMP stack, or Docker)

## Step 1: Install Required Packages

Start by installing the necessary dependencies:

```sh
sudo dnf install php php-cli php-mysqlnd php-xml php-curl php-mbstring php-zip unzip git mysql-server
```

Enable and start MySQL:

```sh
sudo systemctl enable --now mysqld
```

Secure MySQL installation:

```sh
sudo mysql_secure_installation
```

## Step 2: Install WP-CLI

WP-CLI is a powerful tool for managing WordPress from the terminal.

```sh
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
```

Verify installation:

```sh
wp --info
```

## Step 3: Set Up a Local WordPress Environment

There are multiple ways to set up a local WordPress environment on Fedora. The two most common methods are using LocalWP or a LAMP stack.

### Option 1: Using LocalWP

If you installed [LocalWP](https://localwp.com/), create a new WordPress site, navigate to its shell, and proceed with plugin development.

### Option 2: Using a LAMP Stack

Manually set up WordPress by downloading and configuring it:

```sh
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
sudo mv wordpress mysite
sudo chown -R apache:apache mysite
```

Configure Apache and MySQL accordingly.

## Step 4: Create a WordPress Plugin

Navigate to the WordPress plugin directory:

```sh
cd wp-content/plugins/
mkdir my-plugin
cd my-plugin
```

Create a main plugin file `my-plugin.php`:

```php
<?php
/**
 * Plugin Name: My Custom Plugin
 * Description: A simple plugin for testing.
 * Version: 1.0
 * Author: Your Name
 */

if (!defined('ABSPATH')) {
    exit; // Exit if accessed directly
}

function my_custom_plugin_function() {
    echo '<p>Hello from My Custom Plugin!</p>';
}
add_action('wp_footer', 'my_custom_plugin_function');
```

Activate the plugin:

```sh
wp plugin activate my-plugin
```

## Step 5: Debugging and Testing

Enable debugging in `wp-config.php`:

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
@ini_set('display_errors', 0);
```

Check the debug log:

```sh
tail -f wp-content/debug.log
```

Use WP-CLI to check for errors:

```sh
wp plugin verify-checksums my-plugin
```

## Step 6: Automating Development with Composer and PHPCS

Install Composer:

```sh
sudo dnf install composer
```

Install PHPCS and WordPress Coding Standards:

```sh
composer global require squizlabs/php_codesniffer
composer global require wp-coding-standards/wpcs
```

Run PHPCS on your plugin:

```sh
phpcs --standard=WordPress wp-content/plugins/my-plugin
```

## Conclusion

With this setup, you can efficiently develop, test, and debug WordPress plugins on Fedora Linux. Using tools like WP-CLI, PHPCS, and LocalWP ensures a streamlined development workflow.

Happy coding! 🚀

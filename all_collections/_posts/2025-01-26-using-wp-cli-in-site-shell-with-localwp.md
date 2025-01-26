---
layout: post
title: Using WP-CLI in Site Shell with LocalWP on Fedora Linux
date: 2025-01-26
categories: [development, fedora, localwp, wordpress, tools]
---

WP-CLI is a powerful command-line tool for managing WordPress sites. If you're using LocalWP for your local WordPress development, you can leverage WP-CLI directly within the Site Shell. This guide will show you how to make the most of WP-CLI in LocalWP.

---

## What is WP-CLI?

WP-CLI (WordPress Command Line Interface) allows developers to interact with and manage WordPress installations from the terminal. From installing plugins to managing posts, it simplifies repetitive tasks and enhances productivity.

---

## Getting Started with WP-CLI in LocalWP

LocalWP provides a built-in Site Shell feature, making it effortless to use WP-CLI for any site you create within the tool.

### Step 1: Open Site Shell

1. Launch LocalWP.
2. Click on the site you want to work on.
3. Go to the top-right corner and click **"Open Site Shell"**.
4. The terminal window will open, automatically navigating to the site's environment with WP-CLI pre-installed.

### Step 2: WP-CLI Quick Commands

A collection of useful WP-CLI commands for managing your WordPress site effectively.

## 1️⃣ WordPress Core Management
Check WordPress version:
  ```bash
  wp core version
  ```
Update WordPress:
  ```bash
  wp core update
  ```

## 2️⃣ Plugin Management
List installed plugins:
  ```bash
  wp plugin list
  ```
Update all plugins:
  ```bash
  wp plugin update --all
  ```
Install and activate a plugin:
  ```bash
  wp plugin install [plugin-name] --activate
  ```

## 3️⃣ Theme Management
List installed themes:
  ```bash
  wp theme list
  ```
Activate a theme:
  ```bash
  wp theme activate [theme-name]
  ```
Check inactive themes:
  ```bash
  wp theme list --status=inactive
  ```

## 4️⃣ User Management
List all users:
  ```bash
  wp user list
  ```
Create a new user:
  ```bash
  wp user create [username] [email] --role=[role]
  ```
Reset a user’s password:
  ```bash
  wp user update [username] --user_pass=[new-password]
  ```

## 5️⃣ Database Management
Export the database:
  ```bash
  wp db export [filename].sql
  ```
Import a database:
  ```bash
  wp db import [filename].sql
  ```
Optimize the database:
  ```bash
  wp db optimize
  ```

## 6️⃣ Debugging and Testing
Check site status:
  ```bash
  wp site status
  ```
Enable debugging:
  ```bash
  wp config set WP_DEBUG true
  ```
List scheduled Cron jobs:
  ```bash
  wp cron event list
  ```

## 7️⃣ Developer Tools
Generate a custom post type
  ```bash
  wp scaffold post-type [post-type-name]
  ```
Generate a shortcode:
  ```bash
  wp scaffold shortcode [shortcode-name]
  ```
Generate a new plugin:
  ```bash
  wp scaffold plugin [plugin-name]
  ```

For a full list of available commands, type:

```bash
wp help
```

---

## Tips for Efficient Use

Here are some additional tips and best practices for working with WP-CLI in LocalWP:

### Aliases for Faster Access

You can create an alias for WP-CLI commands to save time. For example, add the following to your `.bashrc` or `.zshrc`:

```bash
alias wp="wp --allow-root"
```

Reload the shell:

```bash
source ~/.zshrc
```

### Managing Environment Variables

You can set environment variables in LocalWP to simplify your workflow. For instance, define constants for debugging:

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
```

You can add these to your `wp-config.php` file for development purposes.

---

## Common Errors and Debugging

### Error: "Command not found"

Ensure you have opened the Site Shell provided by LocalWP. WP-CLI is only available in the containerized environment.

### Error: "Database connection failed"

If you encounter database issues, ensure that your LocalWP site is running and that the database credentials in `wp-config.php` match the LocalWP configuration.

---

## Conclusion

Using WP-CLI in LocalWP's Site Shell can significantly speed up your WordPress development process. Whether you need to update plugins, search and replace URLs, or perform database operations, WP-CLI simplifies these tasks. Start integrating it into your workflow today to enhance productivity and efficiency.

---

### Additional Resources

- [WP-CLI Documentation](https://make.wordpress.org/cli/handbook/)

Happy coding! 🚀

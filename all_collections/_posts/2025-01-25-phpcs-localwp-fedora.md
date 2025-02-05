---
layout: post
title: "How to Set Up PHPCS in LocalWP on Fedora Linux"
date: 2025-01-25
categories: [development, fedora, localwp, phpcs, wordpress, tools]
---

If you’re developing WordPress plugins or themes and using [LocalWP](https://localwp.com/) for local development on Fedora, you might need to set up [PHP_CodeSniffer (PHPCS)](https://github.com/squizlabs/PHP_CodeSniffer) to ensure compliance with WordPress Coding Standards. This guide will walk you through the setup process step by step.

---

## 1. Open the LocalWP Site Shell
1. Open LocalWP and select your site.
2. Click on **"Open Site Shell"** to connect to the containerized environment via SSH.

---

## 2. Install PHP_CodeSniffer in LocalWP
Once inside the LocalWP environment, install PHP_CodeSniffer globally using Composer:

```bash
composer global require squizlabs/php_codesniffer
```

Verify the installation by checking the version:

```bash
~/.config/composer/vendor/bin/phpcs --version
```

---

## 3. Install WordPress Coding Standards
Next, install WordPress Coding Standards (WPCS):

```bash
composer global require wp-coding-standards/wpcs
```

Add the WPCS rules to PHPCS:

```bash
~/.config/composer/vendor/bin/phpcs --config-set installed_paths ~/.config/composer/vendor/wp-coding-standards/wpcs
```

Verify that the WordPress standards are installed:

```bash
~/.config/composer/vendor/bin/phpcs -i
```

You should see:

```
The installed coding standards are MySource, PEAR, PSR1, PSR2, Squiz, Zend, WordPress, WordPress-Extra, WordPress-Docs, WordPress-Core
```

---

## 4. Run PHPCS on Your Code
Navigate to your project directory within the LocalWP shell. 

### PHPCS and PHPCBF Commands for WordPress

### 1️⃣ Run PHPCS
Use the `phpcs` command to analyze your code:

```bash
phpcs --standard=WordPress ./path/to/your/file.php
```

### 2️⃣ Optional: Automatic Fixes with PHPCBF
To fix simple coding standard issues automatically, use:

```bash
phpcbf --standard=WordPress ./path/to/your/file.php
```

This will scan/repair your code for WordPress Coding Standards violations.

---

## 5. Set Up VS Code Integration (Optional)
For real-time feedback in Visual Studio Code, you can configure PHPCS:

1. Install the **"PHP Sniffer & Beautifier"** extension.
2. Open your `settings.json` file and add:

```json
"phpcs.executablePath": "/home/user/.config/composer/vendor/bin/phpcs",
"phpcs.standard": "WordPress"
```

With this setup, coding standard violations will be highlighted in the editor.

---

## Summary
By following these steps, you’ve successfully set up PHPCS with WordPress Coding Standards in LocalWP on Fedora. This ensures your code adheres to WordPress best practices and remains maintainable.

Happy debugging! 🚀



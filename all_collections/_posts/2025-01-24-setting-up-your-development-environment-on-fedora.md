---
layout: post
title: "Setting Up Your Development Environment on Fedora Linux: Visual Studio Code and Git"
date: 2025-01-24
categories: [fedora, git, development, visual code, tools]
---

## Setting Up Your Development Environment on Fedora

Fedora Linux is a powerful operating system for developers, offering flexibility, security, and cutting-edge software. In this guide, we’ll walk through how to set up a productive development environment by installing Visual Studio Code and configuring Git.

---

### Step 1: Install Visual Studio Code

Visual Studio Code (VS Code) is a lightweight and powerful code editor popular among developers. To install it on Fedora or other RHEL-based distributions like CentOS, follow these steps:

1. **Add the Yum Repository**:  
   Visual Studio Code is available in the Microsoft yum repository for RHEL, Fedora, and CentOS-based distributions. Set it up by running the following commands:

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc echo -e "[code] name=Visual Studio Code baseurl=https://packages.microsoft.com/yumrepos/vscode enabled=1 gpgcheck=1 gpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null
   ```

2. **Install Visual Studio Code**:  
   After adding the repository, update your package cache and install VS Code using the `dnf` package manager:

   ```bash
   dnf check-update
   sudo dnf install code
   ```

   If you prefer the Insiders edition, replace `code` with `code-insiders`.

3. **Launch VS Code**:  
   Once installed, you can launch VS Code from the application menu or by typing:

   ```bash
   code
   ```

4. **Recommended Extensions**:  
   To enhance your development experience, install these extensions:
   - **PHP Intelephense**: For WordPress and PHP development.
   - **ESLint**: To lint and fix JavaScript code.
   - **Prettier**: For automatic code formatting.
   - **GitLens**: For advanced Git integration.

---

### Step 2: Set Up Git

Git is an essential tool for version control. Let’s set it up on Fedora:

1. **Install Git**:  
   Use the following command to install Git:

   ```bash
   sudo dnf install git
   ```

2. **Configure Git**:  
   Set up your Git identity with the following commands:

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

3. **Generate SSH Key**:  
   Generate an SSH key to authenticate with GitHub or GitLab:

   ```bash
   ssh-keygen -t ed25519 -C "your.email@example.com"
   ```

   Add the generated SSH key to your GitHub/GitLab account. For detailed instructions, check the [GitHub SSH setup guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

4. **Test Your Configuration**:  
   Verify your Git setup:

   ```bash
   git --version
   git config --list
   ```

---

### Conclusion

With Visual Studio Code and Git configured on Fedora, your development environment is ready to handle any project. These tools provide a solid foundation for productivity and version control, making Fedora an excellent choice for developers.

Happy coding! 🚀

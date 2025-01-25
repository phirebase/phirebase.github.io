---
layout: post
title: "How to Install Local by Flywheel on Fedora"
date: 2025-01-23
categories: [fedora, development, wordpress, tools]

---

Local by Flywheel is a fantastic tool for local WordPress development, and the best part is that it now provides a native `.rpm` package for Linux users. Here’s how you can quickly get it installed and running on Fedora.

![Local by Flywheel](/screenshots/local-by-flywheel.png)

---

### Step 1: Download the RPM Package

The Local team offers a prebuilt `.rpm` package for Linux users. You can download it directly from the official website or using the link below:

[Download Local RPM Package](https://cdn.localwp.com/releases-stable/9.1.1+6738/local-9.1.1-linux.rpm)

---

### Step 2: Install the RPM Package

Once the download is complete, open your terminal, navigate to the folder where the file is located, and install it using `dnf`:

```bash
sudo dnf install ./local-9.1.1-linux.rpm
```

#### Step 3: Launch Local by Flywheel

After the installation is complete, Local by Flywheel may not launch directly using the `local` command due to conflicts with the default system behavior. To resolve this, you can create an alias for `local` in your shell configuration.

1. **Locate the Installed Binary**:  
   Use the `which` command to find the path of the Local binary:

   ```bash
   which local
   ```
    The output will typically show something like /usr/bin/local.
2. **Create an Alias:**
    To ensure the local command launches LocalWP, create an alias. Add the following line to your ~/.bashrc file:
    ```bash
    echo 'alias local="/usr/bin/local"' >> ~/.bashrc
    ```
3. **Reload Your Shell Configuration:**
    Apply the changes by reloading your shell configuration:

    ```bash
    source ~/.bashrc
    ```
4. **Launch Local by Flywheel:**
    After creating the alias, you can now use the local command to start LocalWP from the terminal:
    ```bash
    local
    ```

### Step 4: Common Troubleshooting
Missing Dependencies
If Local doesn’t start, you may need to install a few missing dependencies. 

```bash
sudo dnf update
```

Permissions
Make sure you’re running Local as a standard user, not as root. Running it as root can cause issues with file permissions.

## Step 5: Fixing Common Errors
If you encounter the following error while starting a site:

```vbnet
Uh-oh! Unable to start site.
Error: Command failed: ... Can't connect to local MySQL server through socket ...
```
![Local by Flywheel](/screenshots/error-23-40-00.png)  

This happens because of a missing dependency. To resolve this issue, install the libxcrypt-compat package:

```bash
sudo dnf install libxcrypt-compat
```

After installing the dependency, try starting your site again.

### Step 6: Fixing "Open Site Shell" Issue 

On Linux, Local by Flywheel uses `gnome-terminal` to execute the "Open Site Shell" command. If this feature does not work, it is likely because the `gnome-terminal` package is not installed.

1. **Install gnome-terminal**:  
   Run the following command to install the required terminal emulator:

   ```bash
   sudo dnf install gnome-terminal
   ```
After installing gnome-terminal, try using the "Open Site Shell" feature in Local again. It should now function correctly.

### Step 7: Start Developing!
Once Local is up and running, you can create new WordPress sites, import existing ones, or configure your environment to your liking. Local offers features like faster site creation, SSL support, and advanced tools for developers.

## Conclusion
Installing Local by Flywheel on Fedora is now easier than ever, thanks to the native .rpm package. With just a few simple steps, you can enjoy one of the best local WordPress development tools available.

For more information and updates, visit the official Local by Flywheel website.

Happy developing! 🚀

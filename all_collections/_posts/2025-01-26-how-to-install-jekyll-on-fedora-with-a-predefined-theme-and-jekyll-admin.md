---
title: How to Install Jekyll on Fedora with a Predefined Theme and Jekyll Admin
date: 2025-01-26
categories: [jekyll, themes, setup, jekyll-admin]
---

Setting up Jekyll on Fedora is straightforward. This guide will walk you through the process of installing Jekyll, using a predefined theme, and setting up Jekyll Admin for managing your site more easily.

---

## Installing Jekyll on Fedora

1. **Install Required Dependencies**  
   Start by installing Ruby and other necessary packages:

   ```bash
   sudo dnf install ruby ruby-devel @development-tools
   ```

2. **Install Jekyll and Bundler**  
   Once the dependencies are installed, install Jekyll and Bundler using RubyGems:

   ```bash
   gem install jekyll bundler
   ```

3. **Verify Installation**  
   Check that Jekyll and Bundler are properly installed:

   ```bash
   jekyll -v
   bundler -v
   ```

   If the commands return version numbers, you're ready to proceed.

---

## Installing a Jekyll Project with a Theme

You can initialize a Jekyll project using a GitHub repository template that includes your desired theme.

### Using a Repository Template

One option is to directly clone a repository with a pre-configured theme. For example, to use the `jekyll-theme-serial-programmer`:

```bash
git clone https://github.com/sharadcodes/jekyll-theme-serial-programmer.git devblog
```

This command:

- Clones the project with the theme into a folder named `devblog`.

After cloning, navigate to the project directory:

```bash
cd devblog
```

Install the necessary dependencies:

```bash
bundle install
```

Finally, start the local server:

```bash
bundle exec jekyll serve
```

---

## Installing Jekyll Admin

Jekyll Admin provides an easy-to-use web interface for managing your Jekyll site. Follow these steps to install and set it up:

1. **Add `jekyll-admin` to Your `Gemfile`**  
   Open the `Gemfile` in your project directory and add this line:

   ```ruby
   gem "jekyll-admin"
   ```

2. **Install Dependencies**  
   Run the following command to install the new dependency:

   ```bash
   bundle install
   ```

3. **Run the Server with Jekyll Admin**  
   Start the Jekyll server, and Jekyll Admin will be accessible:

   ```bash
   bundle exec jekyll serve
   ```

4. **Access the Admin Interface**  
   Open your browser and navigate to:

   ```
   http://localhost:4000/admin
   ```

   From here, you can manage posts, pages, data files, and more through the Jekyll Admin dashboard.

---

## Conclusion

By following these steps, you can set up Jekyll on Fedora, use a predefined theme, and enhance your workflow with Jekyll Admin. This setup simplifies both the development and management of your Jekyll site.

Happy blogging and site management! 🚀

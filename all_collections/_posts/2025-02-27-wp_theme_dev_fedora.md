---
layout: post
title: "Setting Up a WordPress Theme Development Workflow on Fedora Linux"
published: false
date: 2025-02-27
categories: [development, fedora, wordpress, themes, tools]  
---

## Introduction

Developing WordPress themes on Fedora Linux requires a robust workflow with modern tools. This guide will help you set up a development environment using Gulp, Webpack, and Sass to streamline your theme development process.

## Prerequisites

Ensure you have the following installed:

- Fedora Linux (any recent version)
- Node.js and npm
- WordPress installed locally (LocalWP, LAMP stack, or Docker)
- Basic knowledge of WordPress theme development

## Step 1: Install Node.js and npm

To use Gulp, Webpack, and Sass, you need Node.js and npm.

```sh
sudo dnf install nodejs npm
node -v  # Verify installation
npm -v   # Verify installation
```

## Step 2: Set Up a WordPress Theme

Navigate to the WordPress themes directory:

```sh
cd wp-content/themes/
mkdir my-theme
cd my-theme
```

Create `style.css` and `functions.php`:

```css
/*
Theme Name: My Custom Theme
Author: Your Name
Version: 1.0
*/
```

```php
<?php
function my_theme_enqueue_scripts() {
    wp_enqueue_style('main-css', get_template_directory_uri() . '/dist/main.css', [], '1.0', 'all');
    wp_enqueue_script('main-js', get_template_directory_uri() . '/dist/main.js', [], '1.0', true);
}
add_action('wp_enqueue_scripts', 'my_theme_enqueue_scripts');
```

## Step 3: Initialize npm and Install Dependencies

Run the following command in your theme directory:

```sh
npm init -y
```

Install Gulp, Webpack, and Sass:

```sh
npm install --save-dev gulp gulp-sass sass webpack webpack-cli gulp-uglify gulp-concat gulp-postcss autoprefixer cssnano gulp-rename
```

## Step 4: Configure Gulp for Sass Compilation

Create a `gulpfile.js`:

```js
const gulp = require('gulp');
const sass = require('gulp-sass')(require('sass'));
const postcss = require('gulp-postcss');
const autoprefixer = require('autoprefixer');
const cssnano = require('cssnano');
const rename = require('gulp-rename');

const paths = {
    styles: {
        src: 'src/scss/**/*.scss',
        dest: 'dist/'
    }
};

gulp.task('styles', function () {
    return gulp.src(paths.styles.src)
        .pipe(sass().on('error', sass.logError))
        .pipe(postcss([autoprefixer(), cssnano()]))
        .pipe(rename({ suffix: '.min' }))
        .pipe(gulp.dest(paths.styles.dest));
});

gulp.task('watch', function () {
    gulp.watch(paths.styles.src, gulp.series('styles'));
});

gulp.task('default', gulp.series('styles', 'watch'));
```

Run the Gulp task:

```sh
gulp
```

## Step 5: Configure Webpack for JavaScript Bundling

Create a `webpack.config.js`:

```js
const path = require('path');

module.exports = {
    entry: './src/js/main.js',
    output: {
        filename: 'main.js',
        path: path.resolve(__dirname, 'dist')
    },
    mode: 'production'
};
```

Run Webpack:

```sh
npx webpack
```

## Step 6: Organizing Your Theme Structure

Structure your theme as follows:

```
my-theme/
│── src/
│   ├── scss/
│   │   ├── main.scss
│   ├── js/
│   │   ├── main.js
│── dist/
│   ├── main.css
│   ├── main.js
│── functions.php
│── style.css
│── index.php
│── gulpfile.js
│── webpack.config.js
│── package.json
```

## Step 7: Automate Development with Live Reload

For live reload functionality, install Browsersync:

```sh
npm install --save-dev browser-sync gulp-browser-sync
```

Modify `gulpfile.js`:

```js
const browserSync = require('browser-sync').create();

gulp.task('serve', function () {
    browserSync.init({
        proxy: 'http://your-local-wp.test', // Change this to your local site URL
    });
    gulp.watch(paths.styles.src, gulp.series('styles')).on('change', browserSync.reload);
});

gulp.task('default', gulp.series('styles', 'serve'));
```

Run the task:

```sh
gulp
```

## Conclusion

With this setup, you can efficiently develop WordPress themes on Fedora Linux. Gulp and Webpack streamline CSS and JavaScript compilation, making development faster and more maintainable.

Happy theming! 🎨

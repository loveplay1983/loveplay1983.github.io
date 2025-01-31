---
title: "GitHub pages by Jekyll"
date: 2025-01-30 21:57:00 +0800
categories: [Computer Science]
tags: [Utils]
---

# 1. Jekyll installation
```shell
sudo apt-get install ruby-full build-essential zlib1g-dev

echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

gem install jekyll bundler
```

# 2. Jekyll project structure
The directory structure of a Jekyll site using the Chirpy theme is organized to facilitate efficient content management and customization. Here's an overview of the key directories and their purposes:

- **`assets/`**: Contains static assets such as stylesheets, JavaScript files, and images.
  - **`css/`**: Holds the main stylesheet (`jekyll-theme-chirpy.scss`) that defines the site's appearance.
  - **`img/`**: Stores images, including favicons and other site graphics.

- **`_config.yml`**: The main configuration file for the Jekyll site, where global settings are defined.
- **`_data/`**: Holds YAML files for structured data, such as `contact.yml` and `share.yml`, which can be accessed throughout the site.
- **`Gemfile` and `Gemfile.lock`**: Manage Ruby gem dependencies for the Jekyll site.
- **`_includes/`**: Contains partial templates (e.g., headers, footers) that can be included in other templates or pages.
- **`_layouts/`**: Holds layout templates that define the structure of different types of pages (e.g., posts, pages).
- **`_posts/`**: Contains blog posts in Markdown format, following the naming convention `YEAR-MONTH-DAY-title.md`.
- **`README.md`**: Provides information about the Jekyll site and instructions for setup and customization.
- **`_sass/`**: Contains Sass partials that are compiled into CSS, allowing for modular and maintainable styles.
- **`_site/`**: The output directory where the generated static site is placed after building.
- **`_tabs/`**: Holds Markdown files for navigation tabs, such as "About," "Archives," "Categories," and "Tags."
- **`tools/`**: Contains utility scripts, such as `run.sh` and `test.sh`, for building and testing the site.

To customize the site's appearance, modify the `jekyll-theme-chirpy.scss` file located in the `assets/css/` directory. This file imports various Sass partials from the `_sass/` directory, including `_variables.scss`, `_mixins.scss`, and others, which define the site's styles. By overriding variables or adding custom styles in this file, the site's appearance can be tailored without directly modifying the theme's core files. ([chirpy.cotes.page](https://chirpy.cotes.page/posts/getting-started/?utm_source=chatgpt.com))

For more detailed information on customizing the Chirpy theme, refer to the official documentation. ([chirpy.cotes.page](https://chirpy.cotes.page/posts/getting-started/?utm_source=chatgpt.com)) 




# References
- [Javasript-w3js](https://www.w3schools.com/w3js/default.asp)
- [Chirpy-template](https://github.com/cotes2020)
- [Jekyll-complete-tutorial](https://jekyllrb.com/docs/step-by-step/10-deployment/)
- [GitHub-guidelines](https://docs.github.com/en/pages)
- [How to build your Blog for free on GitHub Pages using Jekyll (Walkthrough)](https://www.youtube.com/watch?v=m1RYsmOMPLs)
- [Front-matter-CMS](https://frontmatter.codes/)
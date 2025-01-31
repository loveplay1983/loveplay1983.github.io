---
title: "Tabs and how does jekyll site work?"
date: 2025-01-31 14:45:00 +0800
categories: [Computer Science]
tags: [Utils]
---

# 1.How is tab order used in Jekyll site

`_tabs` folder - `about.md`
```html
---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---
```

`_includes` folder - `sidebar.html`
```html
{% for tab in site.tabs %}
  <li class="nav-item{% if tab.url == page.url %} active{% endif %}">
    <a href="{{ tab.url | relative_url }}" class="nav-link">
      <i class="fa-fw {{ tab.icon }}"></i>
      {% capture tab_name %}{{ tab.url | split: '/' | last | remove: '/' }}{% endcapture %}
      <span>{{ site.data.locales[include.lang].tabs[tab_name] | default: tab.title | upcase }}</span>
    </a>
  </li>
{% endfor %}
```

- `tab.url`: This represents the URL of the current tab in the loop. It's typically defined in the front matter of the corresponding Markdown file within  the _tabs collection.

- `relative_url Filter`: The relative_url filter is applied to tab.url to ensure that the generated link respects the site's base URL. This is particularly important if  the site is hosted in a subdirectory. For example, if  the site's base URL is /blog and tab.url is /about/, applying the relative_url filter will produce /blog/about/. This ensures that links are correctly formed relative to the site's root. 
JEKYLLRB.COM

- `capture Tag for tab_name`: The {% raw %} {% capture %} {% endraw %} tag is used to extract the tab's name from its URL. By splitting tab.url by '/' and taking the last segment, it captures the tab's identifier, which is then used to fetch the localized tab title from site.data.locales.

> By structuring the _tabs collection and defining each tab's url and title in their respective front matter, this template dynamically generates the sidebar navigation, ensuring that each tab links to the correct page with the appropriate label.

# 2. How are the posts in markdown format connected to the html pages?

In Jekyll, the conversion of Markdown files to HTML is facilitated by a combination of directory structure, configuration files, and the build process. Here's an overview of how this works:

1. **Directory Structure**:
   - **`_posts/`**: This directory contains the blog posts written in Markdown. Each file's name follows the format `YEAR-MONTH-DAY-title.MARKUP`.
   - **`_layouts/`**: Contains templates that define the structure of the pages and posts. For example, a `post.html` layout might include headers, footers, and placeholders for content.
   - **`_includes/`**: Holds reusable snippets of code (e.g., headers, footers) that can be included in the layouts or posts using the Liquid tag {% raw %} {% include file.html %} {% endraw %}.
   - **`_config.yml`**: The main configuration file to set site-wide settings, such as the site's title, author information, and configuration options.

2. **Front Matter**:
   - At the beginning of each Markdown file, there's a section called front matter, enclosed by `---`. This section specifies metadata like the layout to use, the title, and other attributes. For example:
   ```markdown
   ---
   layout: post
   title: "My First Post"
   ---
   ```
   - Jekyll uses this metadata to determine how to process and render the file.

3. **Build Process**:
   - When we run `jekyll build` or `jekyll serve`, Jekyll processes the site as follows:
     - **Reads Configuration**: Loads settings from `_config.yml`.
     - **Processes Files**: Reads the Markdown files in `_posts/` and other directories.
     - **Applies Layouts**: Wraps the content of each Markdown file with the specified layout from `_layouts/`.
     - **Renders Includes**: Inserts content from `_includes/` where specified in the layouts or posts.
     - **Generates HTML**: Converts the combined content into HTML and outputs the final files into the `_site/` directory.

4. **Serving the Site**:
   - The generated HTML files in the `_site/` directory are what get served to visitors. If you're using `jekyll serve`, it starts a local web server that serves these files, allowing us to preview the site locally.

# 3. Example about the buid process in Jekyll 

```markdown
---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---
```

THe default layout is 'page'. However, it is commented out, so Jekyll will search for the defaults configuration in _config.yml file. 

```yml
collections:
  tabs:
    output: true
    sort_by: order

defaults:
  - scope:
      path: "" # An empty string here means all files in the project
      type: posts
    values:
      layout: post
      comments: true # Enable comments in posts.
      toc: true # Display TOC column in posts.
      # DO NOT modify the following parameter unless you are confident enough
      # to update the code of all other post links in this project.
      permalink: /posts/:title/
  - scope:
      path: _drafts
    values:
      comments: false
  - scope:
      path: ""
      type: tabs # see `site.collections`
    values:
      layout: page
      permalink: /:title/
```



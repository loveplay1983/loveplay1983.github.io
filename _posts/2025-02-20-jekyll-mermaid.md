---
title: "DeepSeek local deployment test"
date: 2025-02-20 22:01:00 +0800
categories: [Computer Science]
tags: [Utils]
mathjax: true
mermaid: true
---

## [Jekyll-mermaid](https://github.com/jasonbellamy/jekyll-mermaid)

### Method 1: Using a Jekyll Plugin (e.g. jekyll-mermaid)

1. **Add the Plugin to Your Gemfile:**  
   Open your Gemfile in your Jekyll project and add:  
   ```ruby
   gem "jekyll-mermaid"
   ```
   Then run:
   ```bash
   bundle install
   ```

2. **Enable the Plugin in _config.yml:**  
   Add the plugin under the plugins section:
   ```yaml
   plugins:
     - jekyll-mermaid
   ```
   *(In older Jekyll versions, you might need to use the `gems` key instead.)*

3. **Write Mermaid Diagrams in Your Markdown Files:**  
   ```markdown
   # mermaid
   graph TD;
       A-->B;
       A-->C;
       B-->D;
       C-->D;
   ```

### Method 2: Including Mermaid.js Directly in Your Templates

1. **Include the Mermaid Library:**  
   Edit your Jekyll layout (e.g. `_layouts/default.html`) and add the following script tag in the `<head>` section:
   ```html
   <script type="module">
     import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
     mermaid.initialize({ startOnLoad: true });
   </script>
   ```

2. **Write Mermaid Diagrams in Markdown Files:**  
   ```markdown
   # mermaid
   sequenceDiagram
       participant Alice
       participant Bob
       Alice->>Bob: Hello Bob, how are you?
       Bob-->>Alice: I am good thanks!
   ```



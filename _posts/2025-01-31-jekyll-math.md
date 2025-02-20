---
title: "How to display math expression on the pages using Jekyll"
date: 2025-01-31 22:24:00 +0800
categories: [Computer Science]
tags: [Utils]
mathjax: true
---

# How to render Markdown math expressions on the GitHub Pages site using Jekyll

1. **Ensure Kramdown is the Markdown Processor**:
   GitHub Pages uses Kramdown as the default Markdown processor, which supports LaTeX-style math syntax. Verify that the `_config.yml` file does not specify a different processor. If it does, remove or comment out the `markdown` line to use the default Kramdown processor. ([alanduan.me](https://alanduan.me/random/mathjax/?utm_source=chatgpt.com))

2. **Include the MathJax Script**:
   MathJax is a JavaScript library that renders LaTeX math expressions in web pages. To include MathJax in the Jekyll site:
   - Create a file named `mathjax.html` in the `_includes` directory with the following content:
     ```html
     <script type="text/javascript" id="MathJax-script" async
       src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
     </script>
     ```
     ([deyloop.github.io](https://deyloop.github.io/notebox/20221127114316/?utm_source=chatgpt.com))
   - In the `_layouts/default.html` file, include the `mathjax.html` file within the `<head>` section:
     ```html
     {% if page.mathjax %}
       {% include mathjax.html %}
     {% endif %}
     ```
     ([jojozhuang.github.io](https://jojozhuang.github.io/tutorial/jekyll-math-symbols-with-mathjax/?utm_source=chatgpt.com))

3. **Enable MathJax in Specific Pages**:
   To enable MathJax on pages for math expression:
   - In the front matter of the Markdown file, add:
     ```yaml
     ---
     layout: post
     title: the Post Title
     date: 2025-01-31
     mathjax: true
     ---
     ```
     ([jojozhuang.github.io](https://jojozhuang.github.io/tutorial/jekyll-math-symbols-with-mathjax/?utm_source=chatgpt.com))

4. **Write Math Expressions**:
   Use LaTeX syntax to write math expressions in the Markdown files:
   - Inline math:
     ```markdown
     This is an inline math expression: $$a^2 + b^2 = c^2$$.
     ```
     This is an inline math expression: $$a^2 + b^2 = c^2$$.
   - Display math:
     ```markdown
     This is a display math expression:
     \begin{equation}\int_{a}^{b} f(x) \, dx\end{equation}
     ```
     This is a display math expression:
     \begin{equation}\int_{a}^{b} f(x) \, dx\end{equation}
     ([jojozhuang.github.io](https://jojozhuang.github.io/tutorial/jekyll-math-symbols-with-mathjax/?utm_source=chatgpt.com))

5. **Handle Potential Conflicts**:
   Be aware that some Markdown processors may interfere with MathJax rendering. If issues exist, consider using the `raw` and `endraw` tags to prevent the processor from interpreting math syntax:
   ```markdown
   {% raw %} $$a^2 + b^2 = c^2$$ {% endraw %}
   ```
   ([ishxiao.com](https://ishxiao.com/blog/html/2017/06/29/how-to-support-latex-in-github-pages.html?utm_source=chatgpt.com))


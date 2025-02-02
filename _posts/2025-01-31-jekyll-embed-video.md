---
title: "How to embed self-hosted video on GitHug page by Jekyll"
date: 2025-02-02 16:48:00 +0800
categories: [Computer Science]
tags: [Utils]
mathjax: true
---

# How to embed self-hosted video on GitHug page by Jekyll?

### 1. video tag
```html
<video width="320" height="240" controls autoplay=true loop=true muted=true>
  <source src="https://github.com/loveplay1983/loveplay1983.github.io/raw/refs/heads/main/assets/videos/Hangzhou-zoo.mp4">
</video>
```

### 2. About the src 
- Upload the video file to your github.io repo
- Go/click to where the file is located in the repo, and copy the View raw hyperlink
- Write this code on your html page using the copied link as src (check the video tag code above)


### 3. References
- [self-hosted video on GitHub page by Jekyll](https://medium.com/@ciaranbench/how-to-add-a-video-file-on-github-pages-github-io-website-html-a2e9dd81618a)



---
title: "How to display pdf files on pages using Jekyll"
date: 2025-01-31 22:55:00 +0800
categories: [Computer Science]
tags: [Utils]
mathjax: true
---

While Jekyll doesn't natively support embedding PDFs directly into Markdown files, it can be achieved by using HTML tags within the Markdown content. 

1. **Upload the PDF to the Repository**:
   - Place the PDF file in a directory within the Jekyll project, such as `assets/pdfs/`.

2. **Embed the PDF in the Markdown File**:
   - Use the HTML `<object>` or `<embed>` tag to embed the PDF. For example:
     ```html
     <object data="{{ site.baseurl }}/assets/pdfs/thefile.pdf" type="application/pdf" width="100%" height="600px">
       <p>the browser does not support PDFs. <a href="{{ site.baseurl }}/assets/pdfs/thefile.pdf">Download the PDF</a>.</p>
     </object>
     ```
     Replace `thefile.pdf` with the actual name of the PDF file.

3. **Ensure Correct URL Generation**:
   - Using `{{ site.baseurl }}` ensures that the URL is correctly generated, especially if the site is hosted in a subdirectory. ([stackoverflow.com](https://stackoverflow.com/questions/62206911/jekyll-gh-pages-embed-pdf?utm_source=chatgpt.com))

4. **Alternative Method**:
   - If embedding the PDF directly doesn't work as expected, consider providing a link to the PDF:
     ```markdown
     [Download the PDF](assets/pdfs/thefile.pdf)
     ```
     This approach allows users to download or view the PDF in a new tab.

**Note**: Embedding PDFs using HTML tags like `<object>` or `<embed>` may not work consistently across all browsers and devices. Providing a direct link to the PDF is a more reliable method. ([talk.jekyllrb.com](https://talk.jekyllrb.com/t/embed-pdf-in-github-pages/4527?utm_source=chatgpt.com))

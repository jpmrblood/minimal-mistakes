---
title: Adding Jekyll Search
tags:
  - jekyll
  - search
  - function
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/the-most-terrifying.png
excerpt: Add Jekyll search
---
Add this to any page. I want in the front page. So, I add this to `_layouts/home.html`

```bash
<!-- Html Elements for Search -->
<div id="search-container">
<input type="text" id="search-input" placeholder="search..." />
<ul id="results-container"></ul>
</div>

<!-- Script pointing to search-script.js -->
<script src="/assets/js/search-script.min.js" type="text/javascript"></script>

<!-- Configuration -->
<script>
SimpleJekyllSearch({
 searchInput: document.getElementById('search-input'),
 resultsContainer: document.getElementById('results-container'),
 json: '/search.json'
})
</script>
```

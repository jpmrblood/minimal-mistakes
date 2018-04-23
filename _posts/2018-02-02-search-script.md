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
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Add Jekyll search
---
Add this to any page with search functionality. I want this in the front page of my site.
So, I add the code to `_layouts/home.html`

# Search code

```html
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

Note:

Actually, it was described on the original [Simple Jekyll Search page](https://github.com/christian-fei/Simple-Jekyll-Search). LOL!

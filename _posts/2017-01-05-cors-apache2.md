---
title: CORS in Apache2
tags:
  - apache2
  - site
  - cors
categories:
  - linux
  - apache2
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/01/http-cors.png
  overlay_image: /assets/2017/01/http-cors.png
excerpt: How to enable CORS
---
Browser keep stricter each days. Now, they insist on CORS. I can't enable it in  .htaccess, must do it in sites-enabled.

```ini
<IfModule mod_headers.c>
  <FilesMatch "\.(ttf|ttc|otf|eot|woff|woff2|font.css|css|js)$">
    Header set Access-Control-Allow-Origin "*"
  </FilesMatch>
</IfModule>
```

# Further Read

[Access-Control-Allow-Origin Multiple Origin Domains?](http://stackoverflow.com/questions/1653308/access-control-allow-origin-multiple-origin-domains)

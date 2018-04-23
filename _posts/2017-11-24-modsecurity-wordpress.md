---
title: Whitelisting Wordpress in Apache2
tags:
  - apache2
  - wordpress
  - modsecurity
categories:
  - apache2
  - tips
  - wordpress
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/01/http-cors.png
  overlay_image: /assets/2017/01/http-cors.png
excerpt: How to whitelist
---
Whitelisting Wordpress installation in Apache's HTTPd Mod Security 2.

```ini

<LocationMatch "/wp-admin">
  SecRuleRemoveById 950109 950901 950117 958030 960024 970903 973300 973301 973304 973332 973333 973338 981143 981172 981173 981245 950007 950120 981231
</LocationMatch>

<LocationMatch "/wp-admin/nav-menus.php">
  SecRuleRemoveById 960335
</LocationMatch>

<LocationMatch "/wp-login.php">
  SecRuleRemoveById 950007 950109 950117 950120 950901 981143 981172 981173 970901 970903
</LocationMatch>

<LocationMatch "/wp-content">
  SecRuleRemoveById 950007 950120 958231 970903 981172
</LocationMatch>

<LocationMatch "(/wp-admin/options.php|/wp-admin/theme-editor.php|/wp-content/plugins/)">
  SecRuleRemoveById 950005 950006 950907 958009 959006 959070 960008 960011 960904 973334 973335 973344 973347 981231 981317

  SecRuleRemoveById phpids-17 # Detects JavaScript object properties and methods
  SecRuleRemoveById phpids-20 # Detects JavaScript language constructs
  SecRuleRemoveById phpids-21 # Detects very basic XSS probings
  SecRuleRemoveById phpids-30 # Detects common XSS concatenation patterns 1/2
  SecRuleRemoveById phpids-61 # Detects url injections and RFE attempts
</LocationMatch>

<LocationMatch "/wp-admin/options-general.php">
  SecRuleRemoveById 960335
</LocationMatch>

<LocationMatch "/wp-includes">
  SecRuleRemoveById 950006 950007 950120 959006 960010 960012 970903 981172  

  SecRuleRemoveById phpids-17 # Detects JavaScript object properties and methods
  SecRuleRemoveById phpids-20 # Detects JavaScript language constructs
  SecRuleRemoveById phpids-21 # Detects very basic XSS probings
  SecRuleRemoveById phpids-30 # Detects common XSS concatenation patterns 1/2
  SecRuleRemoveById phpids-61 # Detects url injections and RFE attempts
</LocationMatch>

<LocationMatch "/wp-admin/post.php">
  SecRuleRemoveById 950001 950007 950120 958977 959070 959072 959073 960335 970901 973306 973316 973334 973335 973343 973344 973347 981231 981243 981244 981246 981249 981257 981318 970903 981172 981256
</LocationMatch>

<LocationMatch "/wp-admin/admin-ajax.php">
  SecRuleRemoveById 950911 970901 973306 973316 973334 973335 973344 973347 981231 981257 981318 970903 950007 950120 981172 981242 981244 2100081
</LocationMatch>

<LocationMatch "/wp-admin/async-upload.php|/wp-admin/media-new.php">
  SecRuleRemoveById 200004
</LocationMatch>

<LocationMatch "/favicon.ico">
  SecRuleRemoveById 950007 950120 981172 981243 970903
</LocationMatch>

<LocationMatch "/feed">
  SecRuleRemoveById 970901
</LocationMatch>

<LocationMatch "/xmlrpc.php">
  SecRuleRemoveById 950001 959070 959071 959073 973302 973332 973333 973334 973335 973344 973347 981244 981248 981249 981256 981317 981320
</LocationMatch>
```

# Further Read

https://github.com/wrender/modsecurity-whitelist-apps/blob/master/modsec2.whitelist_app_wordpress.conf

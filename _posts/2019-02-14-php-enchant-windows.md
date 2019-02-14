---
title: Install PHP Enchant on Apache HTTPd Windows
tags:
  - php
  - enchant
  - windows
  - apache
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Setup PHP Enchant on Windows
---

# Install PHP 7.2

Install it on a folder. Don't forget to add that folder to PATH.

Copy `php.ini-production` to `php.ini`

Add to `php.ini`:

```php
extension_dir=c:/php-7.2/ext

extension=enchant
```

Create dir:
`C:\php-7.2\share\myspell\dicts`

Put `en_US.aff` and `en_US.dic` to there. You could search them on the Internet or pull it from Debian source file for Libreoffice Dictionaries package (about 46MB).

## Check if okay

If not well:

```
C:\>php
PHP Warning:  PHP Startup: Unable to load dynamic library 'enchant' (tried: C:\php\ext\enchant (The specified module could not be found.), C:\php\ext\php_enchant.dll (The specified module could not be found.)) in Unknown on line 0
```

Yes, PHP search for extension on those dirs.

If all is well:

```
C:\>php
```

Nothing.

# Apache 2.4

Add

```php
AddHandler application/x-httpd-php .php
AddType application/x-httpd-php .php .html
LoadModule php7_module "C:/php-7.2/php7apache2_4.dll"
PHPiniDir "c:/php-7.2"
```

Restart.

# Source

[Enchant](https://stackoverflow.com/a/29103302)
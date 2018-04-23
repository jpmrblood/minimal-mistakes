---
title: Adding multiple lines with sudo
tags:
  - shell
  - sudo
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Adding multiple lines to a file with sudo.
---
# Overwrite/Make New

When you want a multi line write to a file using sudo:
```bash
$ sudo tee /tmp/test.txt << EOF
LINE 1
LINE 2
...
LINE n
EOF

```

# Append

For appending new lines

```bash
$ sudo tee -a /tmp/test.txt << EOF
LINE 1
LINE 2
...
LINE n
EOF

```
Done.

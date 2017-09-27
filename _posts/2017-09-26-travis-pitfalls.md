---
layout: post
title:  "Travis CI pitfalls"
date:   2017-09-26 11:21:24 +0200
categories: php
tags:
- travis
- travis ci
- ci
---
During implementation of CI infrastructure having PHP, you may face with
different errors and strange behaviours.

# Permission denied error

```
/home/travis/build.sh: line 45: ./some_script.sh: Permission denied
The command "./some_script.sh" failed and exited with 126 during .
```

This error happens if you do not have executable bit on your script

`chmod +x some_script.sh` should fix this error

# Environment variables

To be able to use environment variables in your scripts, you need to click
`More options -> Settings` in Travis interface and add it.

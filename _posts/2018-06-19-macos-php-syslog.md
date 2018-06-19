---
layout: post
title:  "Writing logs to syslog with PHP and Monolog on Mac OS"
date:   2018-06-19 15:00:00 -0500
categories: php
tags:
- php
- syslog
- mac os
---

Most *nix-based sustems support syslog storage for different types of system logs.
On Mac OS it's also present and we can use it.

# Monolog

Syslog implementation exists as part of [Sysloh Handler](https://github.com/Seldaek/monolog/blob/master/src/Monolog/Handler/SyslogHandler.php)

To use it let'c create Monolog object and configure handler:

```php
    $monolog = new Monolog('default');
    $monolog->pushHandler(
        new SyslogHandler('My log')
    );
```

# Console

Once you configure this handler, open `Console` application and filter by:
- `library`: php

You will see something like this:

![Console]({{ "/assets/images/syslog.png" }})

---
layout: post
title:  "Installing supervisor on Mac OS"
date:   2019-07-16 15:34:00 -0500
categories: php
tags:
- supervisor
- unix
- mac os
- laravel
---

Supervisor is powerful process manager for Unix systems. You can get a lot of advantages by using it.

# Installation

```bash
brew install supervisor
```

# Configuration

* `/usr/local/etc/supervisord.ini` - default configuration file. 
* `/usr/local/etc/supervisor.d` - directory for your custom `*.ini` files

or automatically on your system start

To view active configuration, run:

```bash
echo_supervisord_conf
```

# Run

## Manual run

```bash
supervisord -c /usr/local/etc/supervisord.ini
```

## Run on system's startup

```bash
brew services start supervisor
```

# Web control panel

To be able to monitor and manage your processes via browser, you'll have to open `/usr/local/etc/supervisord.ini` and modify these lines:

```bash
[inet_http_server]         ; inet (TCP) server disabled by default
port=127.0.0.1:9001        ; ip_address:port specifier, *:port for all iface
username=user              ; default is no username (open server)
password=1234              ; default is no password (open server)
``` 

# Typical errors

> unix:///usr/local/var/run/supervisor.sock no such file

To fix this error, kill the running process:

```bash
ps -ef | grep supervisor
pkill -f supervisord
```

Source: [https://www.cnblogs.com/c-x-a/p/10231065.html](https://www.cnblogs.com/c-x-a/p/10231065.html)

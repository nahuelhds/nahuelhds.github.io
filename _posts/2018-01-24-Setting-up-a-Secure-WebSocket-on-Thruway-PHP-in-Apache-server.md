---
lang: en
title: Setting up a Secure WebSocket on Thruway (PHP) in Apache server
excerpt: >-
  If you have a working websocket server voryx/Thruway you probably want to know
  how to configure it to make it work with secure websocket…
date: '2018-01-24T03:17:32.847Z'
categories:
  - server
keywords:
  - apache
  - websocket
  - php
  - thruway
  - tls
  - ssl
---

![](img/1__N08XZ82dODX22Nuw0H1J0w.jpeg)

If you have a working websocket server [voryx/Thruway](https://github.com/voryx/Thruway) you probably want to know how to configure it to make it work with secure websocket protocol (wss://)

**It’s important to notice that this configuration doesn’t require any modification in the Wamp server. You only need to modify the Apache config and the Wamp client that will use the secure protocol.**

I’ll share my working config, but the main guide for reach to it [I got it in this GitHub issue](https://github.com/voryx/Thruway/issues/66).

**Important:** the communication between Apache and Thruway won’t be encrypted, but it will be encrypted from the browser to Apache

### Some context

1.  My Wamp Server works under port `9090` (listening `0.0.0.0`)
2.  My AutobahnJS client connects fine at `ws://127.0.0.1:9090`
3.  I want to use the very same 443 port for the wss connection as well.

### Apache config

#### httpd.conf

You need to modify the`httpd.conf` file and enable the following modules:

1.  mod\_proxy
2.  mod\_proxy\_wstunnel

#### httpd-vhost.conf

Then you need to configure the virtual host for HTTPS and WSS proxy redirection:

```apache
<VirtualHost *:443>
  # Common SSL Config
  ServerName my-site.test
  SSLEngine on
  SSLCertificateFile "/usr/local/etc/httpd/server.crt"
  SSLCertificateKeyFile "/usr/local/etc/httpd/server.key"
  DocumentRoot "/Users/nahuelhds/Sites/my/site"
  <Directory  "/Users/nahuelhds/Sites/my/site">
    Options +Indexes +FollowSymLinks +MultiViews
    AllowOverride All
    Require local
  </Directory>
  # Websocket proxy
  # wss redirects to working ws protocol
  ProxyPass /wss ws://127.0.0.1:9090 retry=0 keepalive=On 
  ProxyPassReverse /wss ws://127.0.0.1:9090 retry=0 
</VirtualHost>
```

Restart Apache to impact the changes.

### WebSocket Client URL

Now you can use this URL for the Secure WebSocket: `wss://my-site.test/wss`

You can test if the WebSocket works at [http://www.websocket.org/echo.html](http://www.websocket.org/echo.html)

---
lang: en
title: Enable SSL with OpenSSL and WAMP on Windows 10
excerpt: >-
  If you need to enable SSL for your local development process on Windows, you
  know that can be a nightmare…
date: '2019-05-12T22:22:02.318Z'
categories: 
  - wamp
keywords:
  - ssl
  - windows10
  - openssl
  - wamp
---

![](img/0__HC__ouHIX5ypCpxsF.jpg)

This is my environment: Windows 10 x64, WampServer Version 3.0.4 64bits and Apache 2.4.18

### TL;DR

[The instructions are on this post inside the WampServer forum.](http://forum.wampserver.com/read.php?2,137505,137522#msg-137522)

If you can start Apache, possibly there is something bad in your config. My issues are described in the next section. You can see your errores executing `httpd` directly on **cmd**.

```
cd \\wamp\bin\apache\apachex.y.z\binhttpd -t
```

That will show you the errors inside the configuration file and the line as well.

#### Important

It’s necessary to use a non-native **OpenSSL** version from WAMP. I downloaded mine [from SourceForge’s page](https://sourceforge.net/projects/openssl/). The downloaded file was [https://ufpr.dl.sourceforge.net/project/openssl/openssl-1.0.2j-fips-x86\_64/openssl-1.0.2j-fips-x86\_64.zip](https://ufpr.dl.sourceforge.net/project/openssl/openssl-1.0.2j-fips-x86_64/openssl-1.0.2j-fips-x86_64.zip)

### Errors that I’ve faced

#### Native OpenSSL on WAMP: “Can’t find ordinal (…)”

On _WampServer 64bits_, the **OpenSSL** executable doesn’t work on _Windows 10 64bits_, so you need to download a working version for it.

My particular error was “The ordinal 113 could not be located in the dynamic link library”. The solution was to install OpenSSL on my own, like described above.

#### WAMP httpd: “invalid command SSLCipherSuite”

Uncomment the line from the `httpd.conf` file.

```
LoadModule ssl_module modules/mod_ssl.so
```

You can follow the instructions from the source.

**Source:** [http://impradeep.com/invalid-command-sslciphersuite-perhaps-misspelled-or-defined-by-a-module-not-included-in-the-server-configuration/](http://impradeep.com/invalid-command-sslciphersuite-perhaps-misspelled-or-defined-by-a-module-not-included-in-the-server-configuration/)

#### WAMP httpd: “Cannot load modules/mod\_ssl.so into server”

Two possible paths here. **The seconds worked for me**.

**Include the OpenSSL’s DDL in the Windows directory**

You have to install a different OpenSSL version. You can see this StackOverlow’s answer and follow the instructions: [http://stackoverflow.com/questions/40017498/cannot-load-modules-mod-ssl-so-into-server](http://stackoverflow.com/questions/40017498/cannot-load-modules-mod-ssl-so-into-server)

**Replace libeay32.dll and ssleay32.dll on the Apache directory**

It’s weird but those files _libeay32.dll_ and _ssleay32.dll_ that WAMP 64 ships doesn’t work with the SSL module. You need to download an Apache 32bits version and copy & paste them at `\\wamp\bin\apache\apachex.y.z\bin`.

I took the files [from this Apache version](https://www.apachelounge.com/download/win32/).

Explicitly, this link: [https://www.apachelounge.com/download/win32/binaries/httpd-2.2.32-win32.zip](https://www.apachelounge.com/download/win32/binaries/httpd-2.2.32-win32.zip).

**Source:** [http://serverfault.com/questions/477706/apache-ssl-on-64-bit-windows-not-a-valid-win32-application](http://serverfault.com/questions/477706/apache-ssl-on-64-bit-windows-not-a-valid-win32-application).

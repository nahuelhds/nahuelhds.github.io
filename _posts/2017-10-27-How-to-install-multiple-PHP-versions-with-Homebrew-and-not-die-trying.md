---
lang: en
title: How to install multiple PHP versions with Homebrew and not die trying…
description: May 2019 update
date: '2017-10-27T14:13:39.928Z'
categories:
  - brew
keywords:
  - homebrew
  - php
  - multiple-php
---

![](img/1__ZDOzg6V661UtBKQiGRWVQw.png)

### May 2019 update

By the time of the original post, what I’ve written made sense as they were related to some problems I faced when following that instructions.

Things changed a lot since then and even those problems are not there anymore!

So I can only recommend to [read the original post](https://getgrav.org/blog/macos-sierra-apache-multiple-php-versions) from Grav’s blog. It’s always up-to-date and it contains the best instructions.

Cheers!

### Original post (October 2017)

I’m a new MacOS dev user.

As expected, the first thing I needed to do was to install **MAMP** (**M**acOS, **A**pache, **M**ariaDB/**M**ySQL y **P**HP). The thing is I wanted multiple PHP versions because of the mix of legacy and new projects. A friend recommended me to [follow this guide from Grav’s blog, which is gold](https://getgrav.org/blog/macos-sierra-apache-multiple-php-versions).

Anyway, there are some minor issues that I had while following it.

### PHP extensions— Build from source

It’s mandatory to install the PHP extensions with the `--build-from-source` option. Otherwise, [it’ll throw an error](https://github.com/Homebrew/homebrew-php/issues/2475). So, wherever the guide says “install an extension” the final commands should be:

```sh
brew install php{xy}-{extension} --build-from-source
```

Where as:

*   **xy:** PHP version: 55, 56, 70 o 71.
*   **extension:** specific module: apcu, opcache, yaml or xdebug

If you already did install them, then just use the`reinstall` command.

### SSL Certificate

The guide forgets to mention that Apache needs to be listening the port, so you need to add the command `Listen 443` after the line that says `Listen 80`

### Old MySQL support en PHP5.5 y PHP5.6

This was tricky and it was so simple at the end…

![](img/1__9pqxqRnUXF09vIcHX__BY0g.png){: .img-responsive }

The old mysql extension (mysql\_\*) doesn’t come pre-installed with Homebrew PHP (as it does happen with mysqli\_\* extension). For worse, when you try to install it with the option `--with-libmysql` it doesn’t find some libraries at `/usr/local/bin` so it doesn’t install at all. [Happily, Github exists](https://github.com/Homebrew/homebrew-php/issues/4501#issuecomment-337139957).

So, in resume, you first need to install MySQL:

```sh
brew install mysql
```

Then, you need to stop the MariaDB service, unmount it and then mount MySQL.

```sh
brew services stop mariadb  
brew unlink mariadb  
brew link mysql
```

Once you do this, you have to go to `/usr/local/lib` and duplicate and rename the following files:

```sh
libmysqlclient.a     -> libmysqlclient_r.a
libmysqlclient.dylib -> libmysqlclient_r.dylib
```

Now you can install PHP with the `— with-libmysql` option:

```sh
brew install php55 --with-httpd --with-libmysql  
brew install php56 --with-httpd --with-libmysql
```

If you already installed php55 or php56, just use `reinstall` instead of `install`

### Done!

Happy coding.

![](img/1__o0RaJxltpHX03VGW9F__vrg.png){: .img-responsive }

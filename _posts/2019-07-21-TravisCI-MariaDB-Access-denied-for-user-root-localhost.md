---
lang: en
title: "[Solved] \"ERROR 1698 (28000): Access denied for user 'root'@'localhost'\" on MariaDB in Travis CI"
categories:
  - mariadb
keywords:
  - travis-ci
  - travis
  - root
  - localhost
  - access-denied
---

If you're receiving **"ERROR 1698 (28000): Access denied for user 'root'@'localhost'"** on TravisCI with MariaDB database, you need to use `sudo` in the line execution. Yeah. Just that.

I had this `travis.yml` file

```yaml
addons:
  mariadb: 10.4

before_script:
  - mysql -e 'create database testing;'
```

Notice the `mysql -e 'create database testing;'` line. The fix was using `sudo`

```yaml
addons:
  mariadb: 10.4

before_script:
  - sudo mysql -e 'create database testing;'
```

And that's it. Hope it helps!

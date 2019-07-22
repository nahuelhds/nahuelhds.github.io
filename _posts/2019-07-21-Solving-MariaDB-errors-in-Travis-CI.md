---
lang: en
title: "Solving MariaDB errors in Travis CI"
excerpt: >-
  Some errors I've faced while configuring and deploying on Travis CI
categories:
  - mariadb
keywords:
  - travis-ci
  - travis
  - root
  - localhost
  - access-denied
---

## ERROR 1698 (28000): Access denied for user 'root'@'localhost'

You need to use `sudo` in the line execution. Yeah. Just that.

I had this `.travis.yml` file

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

## SQLSTATE[HY000] [1698] Access denied for user 'travis'@'localhost'

This error happens because Travis by default uses `dist: xenial` which is not fully compatible with the MariaDB addon yet.

The solution is setting `dist: precise` in your `.travis.yml` file

```yaml
dist: precise

# ... rest of your config file
```

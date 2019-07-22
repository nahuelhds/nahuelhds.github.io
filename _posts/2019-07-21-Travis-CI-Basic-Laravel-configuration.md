---
lang: en
title: "Basic Travis CI configuration for Laravel"
excerpt: >-
  A minimum configuration file for your Laravel project
categories:
  - travis-ci
keywords:
  - laravel
---

After some hours for trial and error, I've came up with this basic `.travis.yml` file ready to work with my Laravel project.

**Note:** my Laravel is 5.8 version and works with MariaDB and PHP 7.2.

```yml
# .travis.yml
dist: precise

language: php

php:
  - 7.2

addons:
  mariadb: 10.4

cache:
  directories:
    - node_modules
    - vendor

before_script:
  - cp .env.travis .env
  - sudo mysql -e 'CREATE DATABASE testing;'
  - composer self-update
  - composer install --no-interaction
  - php artisan migrate --no-interaction -vvv

script:
  - vendor/bin/phpunit

```

The `.env.travis` file is versioned and contains the following code.

```apache
# .env.travis

APP_NAME=Laravel
APP_ENV=testing
APP_KEY=base64:Dhtsut2yoe1Oc7Glgl4zPrGLQEKECbi3NoRNQh2N4/c=
APP_DEBUG=true
APP_URL=http://localhost/

DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=testing
DB_USERNAME=travis
DB_PASSWORD=

BCRYPT_ROUNDS=4
CACHE_DRIVER=array
MAIL_DRIVER=array
QUEUE_CONNECTION=sync
SESSION_DRIVER=array
```

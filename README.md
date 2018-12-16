# docker-laravel-ci

![](https://img.shields.io/github/license/GuessEver/docker-laravel-ci.svg)
[![Build Status](https://travis-ci.com/GuessEver/docker-laravel-ci.svg?branch=master)](https://travis-ci.com/GuessEver/docker-laravel-ci)
![](https://img.shields.io/docker/automated/guessever/laravel-ci.svg)
![](https://img.shields.io/docker/build/guessever/laravel-ci.svg)

Laravel docker container for ci test, it helps you to speed up test process

## Usage

### gitlab-ci

```yml
image: guessever/laravel-ci
services:
  - mysql:5.7

variables:
  MYSQL_DATABASE: database_name
  MYSQL_ROOT_PASSWORD: root

cache:
  paths:
  - vendor/

test-migration:
  script:
  # Install project dependencies.
  - composer install

  # Set up project configuration
  - cp .env.ci .env

  # Migrate to database
  - php artisan migrate
```

### bitbucket-pipeline
```yml
image: guessever/laravel-ci

definitions:
  caches:
    bundler: vendor/
  services:
    mysql:
      image: mysql:5.7
      environment:
        MYSQL_DATABASE: database_name
        MYSQL_ROOT_PASSWORD: root

caches:
  - bundler

pipelines:
  default:
    - step:
        name: test build
        services:
          - mysql
        script:
          # Install project dependencies.
          - composer install

          # Set up project configuration
          - cp .env.ci .env

          # Migrate to database
          - php artisan migrate
```

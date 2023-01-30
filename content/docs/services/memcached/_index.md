---
title: "Memcached (Object cache)"
description: "Everything you need to know about configuring Memcached"
---

## Overview

Memcached is a general-purpose memory cache infrastructure daemon. It can improve Drupal application performance by moving Drupal’s standard caches out of the database and by caching the results of other expensive database operations.

The most common use of Memcached with Drupal is storing Drupal’s cache tables in Memcached instead of in the application database. Storing Drupal’s cache tables in Memcached reduces the load on the database with every page load.

## Environment Variables

The format exposed in the `DP_MEMCACHED` environment variables:

```json
{
  "host": "memcached",
  "port": 11211,
  "engine": "memcached",
  "version": "1.6.10",
  "diskSpace": "5Gi",
  "parameters": {
    "MEMCACHED_CACHE_SIZE": "128Mi",
    "MEMCACHED_MAX_CONNECTIONS": 1000,
    "MEMCACHED_THREADS": 2
  }
}
```

## Usage example

### Drupal 8

#### 1. Install `PECL Memcached` extensions

If you use DevPanel php images, you can skip this step.

#### 2. Install `drupal/memcached` module

```shell
composer require drupal/memcache
```

#### 3. Add these lines at the end of `settings.php` file

```php
$settings['memcache']['servers']     = ['memcached:11211' => 'default'];
$settings['memcache']['bins']        = ['default' => 'default'];
$settings['memcache']['key_prefix']  = get('DP_APP_NAME') ? get('HOSTNAME');
$settings['cache']['default']        = 'cache.backend.memcache';
$settings['cache']['bins']['render'] = 'cache.backend.memcache';
```

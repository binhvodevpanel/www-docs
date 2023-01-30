---
menuTitle: "Deploy to VPS"
title: "Deploy Drupal 7 to VPS"
description: "Everything you need to know how to deploy an Drupal 7 activated application on Devpanel to a VPS"
weight: 7
---

The goal of this guide is to show you how to deploy a **Drupal 7** activated application to a connected VPS

## Before you begin

To follow this guilde, you need:

- A Drupal 7 application is activated on DevPanel.
- A VPS on DevPanel. You can see how to connect a VPS to DevPanel [here](/)

## Instructions

### Edit the `settings.php` file

By default, we create Drupal 7 application by using `drush -y site-install` which is in `.devpanel/init.sh` file. Therefore, the database configuration is added to the `sites/default/settings.php` in plain text. You need to change it to use pre-environment variables. Please! look for the `$database` variable in your `settings.php` file. 

It usually looks like

```php
$databases = array (
  'default' => 
  array (
    'default' => 
    array (
      'database' => 'cjahxlepgd',
      'username' => 'qfjxtmaxfb',
      'password' => 'xxxxxx',
      'host' => 'devpanel-cluster-xxxx.xxxx.xxx',
      'port' => '',
      'driver' => 'mysql',
      'prefix' => '',
    ),
  ),
);
```

Replace by:

```php
$databases['default']['default'] = [
  'database' => getenv('DB_NAME'),
  'username' => getenv('DB_USER'),
  'password' => getenv('DB_PASSWORD'),
  'host' => getenv('DB_HOST'),
  'port' => '3306',
  'driver' => 'mysql',
  'prefix' => '',
  'collation' => 'utf8_general_ci',
];
```

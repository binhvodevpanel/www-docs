---
title: "Solr"
description: "Everything you need to know about configuring Solr"
---

## Overview

Solr is highly reliable, scalable and fault tolerant, providing distributed indexing, replication and load-balanced querying, automated failover and recovery, centralized configuration and more. Solr powers the search and navigation features of many of the world's largest internet sites.

## Environment Variables

The format exposed in the `DP_SOLR` environment variables:

```json
{
  "host": "solr",
  "port": 8983,
  "engine": "apache_solr",
  "version": "8.9.0",
  "diskspace": "10Gi",
  "username": "admin",
  "password": "<random_string>"
}
```

## Usage example

### Drupal 8

#### 1. Install _PECL Memcached_ extensions

If you use DevPanel php images, you can skip this step.

#### 2. Install `drupal/search_api_solr` module and dependencies

```shell
composer require symfony/event-dispatcher:~3.4.0 solarium/solarium:^6.1 drupal/search_api_solr:^4.2
```

#### 3. Setup Search API

Navigate to **Drupal Admin Panel > Configuration > Search and metadata > Search API**

1. Click **+ Add server**
2. At **Backend** options, choose **Solr**
3. At **CONFIGURE SOLR BACKEND** enter informations below
   1. **Solr Connector:** `Basic Auth`
   1. **Solr host:** `SOLR_HOST_GENERATED_BY_DEVPANEL`
   1. **Solr port:** `8983`
   1. **Solr path:** `/`
   1. **Solr core:** `devpanel`
   1. **Username:** `devpanel`
   1. **Password:** `SOLR_PASSWORD_GENERATED_BY_DEVPANEL`
4. **Save** and create your index

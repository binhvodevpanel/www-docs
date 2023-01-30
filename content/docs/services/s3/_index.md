---
title: "S3"
description: "Everything you need to know about configuring S3"
---

## Overview

Amazon Simple Storage Service (Amazon S3) is storage for the Internet. It is designed to make web-scale computing easier.

## Environment Variables

The format exposed in the `DP_S3_BUCKET` environment variables:

```json
{
  "bucket": "example-bucket",
  "region": "us-east-1",
  "access_key": "<random_string>",
  "secret_key": "<random_string>",
}
```

## Usage example

#### 1. Installing S3FS Module

##### Drupal 8

```shell
composer require drupal/s3fs
```

##### Drupal 9

```shell
composer require 'drupal/s3fs:^3.0@beta'
```

#### 2. Enable S3FS Module by `drush cli`

```shell
drush pm:enable s3fs
```

#### 3. Add the following to the end of the “settings.php”.

```php
# S3FS setting
$config['s3fs.settings']['bucket'] = 'your bucket name';
$config['s3fs.settings']['public_folder'] = 'your key name';
$config['s3fs.settings']['region'] = 'bucket region';

$settings['s3fs.access_key'] = 'your access key';
$settings['s3fs.secret_key'] = 'your secret key';

$settings['s3fs.use_s3_for_public'] = TRUE;
$config['s3fs.settings']['use_https'] = TRUE;
```

#### 4. Configure S3FS to take over file system:

Now you may want this S3FS module to take over the public file system. Just open the Avanced Configuration Options section and select Use S3 for public:// files . Just tick and save and the module will take care of the rest.

![S3 Public Private](/images/services/s3/s3-public-private.jpeg)

#### 5. Clear the cache and try the first file upload

Now turn into the Actions tab and hit Refresh file metadata cache.

![S3 Clear Cache](/images/services/s3/s3-clear-cache.jpeg)

#### 6. Sync existing files to S3

Also on the Actions tab, there is a button to Copy local public files to S3 . Just hit it and the uploading process will run in batch. If you have not many existing files, just wait for a few hours and it will be ok.

![S3 Copy Local](/images/services/s3/s3-copy-local.jpeg)


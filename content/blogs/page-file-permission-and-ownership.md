---
title: "File permissions and ownership"
description: "Setting the file permissions on your server can help improve the security of your site. The permissions that are used may vary based on your server configuration, your level of access, and the way you intend to use your site."
weight: 2
---

Setting the file permissions on your server can help improve the security of your site. The permissions that are used may vary based on your server configuration, your level of access, and the way you intend to use your site.

## File Permission Level

There are two levels of file permission on DevPanel:

- **Stricter permissions**: Where the web server user (**www-data**) cannot write files. A separate user account (**default user of code-server**) owns the files.
- **Looser permissions**: Where the web server user and the owner of the files is the same (**www** user).

## Pros and Cons

- **Looser permissions**:
  - **Pros**:
    - Easy to understand the structure of application file system.
    - Do not needs to understand too depthly about file system permission in Linux.
    - Easy to upgrade the **core/plugins/modules/extensions** of CMS (**Drupal/Backdrop/Wordpress**) on the UI of CMS applications.
  - **Cons**:
    - Malicious user uploads script file / crafts URL that includes external script file
    - System executes contents of script without allowed of the administrator
    - Malicious user owns system
- **Stricter permissions**:
  - **Pros**:
    - Prever to execute unkown script
    - Limit the damage that malicious users gain the ability to execute arbitrary PHP code.
  - **Cons**:
    - Maybe disable the ability to download/upgrade **core/plugins/modules/extentions** of CMS through the user interface.
    - Rerquires FPT/SSH access that DevPanel does not support yet.

## Check File Permission Level

It has serveral way to check file permission level. You can run below commands to do it:

- Open **Terminal** on DevPanel **Code-Server**, then run `php -i | grep "APACHE_RUN_USER";`, `php -i | grep "APACHE_RUN_GROUP";`. It shows you the user of webserver using.

```shell
$ php -i | grep "APACHE_RUN_USER"

APACHE_RUN_USER => www-data
$_SERVER['APACHE_RUN_USER'] => www-data
$_ENV['APACHE_RUN_USER'] => www-data
```

```shell
$ php -i | grep "APACHE_RUN_GROUP"

APACHE_RUN_GROUP => www-data
$_SERVER['APACHE_RUN_GROUP'] => www-data
$_ENV['APACHE_RUN_GROUP'] => www-data
```

- Then continue to run `ls -alh`

```shell
$ ls -alh

total 120K
drwxrwxr-x 11 www  www-data 4.0K Feb  3 02:48 .
drwxr-xr-x  1 root root     4.0K Sep 28  2021 ..
drwxrwxr-x  2 www  www-data 4.0K Feb  3 02:31 .devpanel
-rw-rw-r--  1 www  www-data  554 Feb  3 02:32 .editorconfig
-rw-rw-r--  1 www  www-data  180 Feb  3 02:32 .gitattributes
-rw-rw-r--  1 www  www-data 6.3K Feb  3 02:32 .htaccess
drwxrwxr-x  2 www  www-data 4.0K Feb  3 02:31 .tugboat
-rw-rw-r--  1 www  www-data  18K Feb  3 02:31 LICENSE.txt
-rw-rw-r--  1 www  www-data 5.2K Feb  3 02:31 README.md
drwxrwxr-x  9 www  www-data 4.0K Feb  3 02:31 core
drwxrwxr-x  3 www  www-data 4.0K Feb  3 02:46 drush
drwxrwxr-x  7 www  www      4.0K Feb  3 02:50 files
-rw-rw-r--  1 www  www-data  592 Feb  3 02:53 index.php
drwxrwxr-x  2 www  www-data 4.0K Feb  3 02:31 layouts
drwxrwxr-x  2 www  www-data 4.0K Feb  3 02:31 modules
-rw-rw-r--  1 www  www-data 1.2K Feb  3 02:31 robots.txt
-rw-r--r--  1 www  www       21K Feb  3 02:48 settings.php
drwxrwxr-x  2 www  www-data 4.0K Feb  3 02:31 sites
drwxrwxr-x  2 www  www-data 4.0K Feb  3 02:31 themes
```

- If the owner and group of files and directory is difference with the apache user and group, It is **Stricter permissions**. Otherwise, It is Looser permissions, when they are same.

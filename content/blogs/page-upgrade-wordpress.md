---
title: "How to Check & Upgrade to latest Wordpress Version"
description: "How to Check & Upgrade to latest Wordpress Version"
weight: 2
---

WordPress is a free and open-source content management system written in hypertext preprocessor language and paired with a MySQL or MariaDB database with supported HTTPS.

## How to Check Your Current WordPress Version

There are multiple ways to check your website’s current WordPress version. This section will demonstrate the three fastest methods to do so.

### Check Wordpress Version on WP-Admin Dasboard

You can check your wordpress site version in the admin dashboard by following the steps below:

- **Log in** to your Wordpress Admin Dashboard

![Login page](/images/blogs/page-upgrade-wordpress/wp-login.jpg)

- In the **Home** page of Wordpress Admin Dashboard, locate the **At a Glance** section

![At A glance](/images/blogs/page-upgrade-wordpress/at-a-glance.jpg)

- You will find your Wordpress version

### Check Wordpress Version by WP-CLI

The WP-CLI is a tool that enables you to interact with your WordPress site directly by using commands in a text-based interface. You can easy to show your Wordpress by using **wp-cli** and **code-server** on DevPanel

- Open the **code-server** of your application on DevPanel

![Codeserver](/images/blogs/page-upgrade-wordpress/code-server.jpg)

- Open **terminal** on **code-server**

![Vscode terminal](/images/blogs/page-upgrade-wordpress/vs-code-terminal.jpg)

- Run commands `wp core version`

```shell
$ wp core version
5.9.3 # <= This is the current verson of your wordpress application
```

## How to Upgrade to the Latest WordPress Version

When we develop on DevPanel, we face with some permission issuse in some case. This is because DevPanels has 2 users in one container (**www** user is the default user of **code-server**, and **www-data** is default user of webserver). Therefore, To work well we need to run several commands below to correct file permission to all of files in the **$WEB_ROOT**.

```shell
sudo find $WEB_ROOT -type d -exec chmod 775 {} \;
sudo find $WEB_ROOT -type f -exec chmod 664 {} \;
```

After correct file permission to all of file we can upgrade wordpress by following steps below:

- Go to your WordPress admin dashboard.
- Locate the "**At a Glance**" widget.
- You’ll see your current WordPress version, and if it’s outdated, you’ll see the "**Update to 6.1.1**" button right next to it.

![At A glance](/images/blogs/page-upgrade-wordpress/at-a-glance.jpg)

- Click on the "**Update to 6.1.1**" button.

- Back up your database and files before updating your version. Visit the [Updating WordPress](https://wordpress.org/documentation/article/updating-wordpress/) documentation page for more information.

- Click the "**Update Now**" button.

![Update now](/images/blogs/page-upgrade-wordpress/update-now.jpg)

- Your WordPress website will be updated to the latest 6.1.1 version in less than a minute.

![Wordpress upgrade successfully](/images/blogs/page-upgrade-wordpress/wordpress-6-1.jpg)
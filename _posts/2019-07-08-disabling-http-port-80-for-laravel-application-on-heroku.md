---
layout: post
title: "Disabling HTTP (port 80) for Laravel application on Heroku"
description: "Disabling HTTP (port 80) for Laravel application on Heroku"
category: "laravel"
tags: [Heroku, Laravel, SSL]
---
{% include JB/setup %}

Heroku is a nice platform especially for small projects. It gets you up and running fairly quickly and configurations are very easy. I however struggled with disabling HTTP in my last project that I used Laravel.

It turned out that Heroku does not have an explicit way of disabling HTTP and the way out is through [Apache's ReWriteRule flags](https://httpd.apache.org/docs/2.4/rewrite/flags.html).

To do so in Laravel, edit the **.htaccess** file inside the **./public** directory and add the following lines:

```apache
    RewriteCond %{HTTP:X-Forwarded-Proto} !https
    RewriteCond %{HTTPS} off
    RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301,NE]
```
And that should redirect HTTP requests to HTTPS url.

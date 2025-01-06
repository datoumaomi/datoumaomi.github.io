---
layout: post
title:  "修改WordPress地址导致无法登录的解决方案"
categories: IT
tags:  WordPress
author: 大头猫米
---

转载自
https://cuijiahua.com/blog/2017/10/website_1.html

一、误操作

WordPress地址(URL)，不能随便更改！（解决方案）

在后台的设置里，WordPress地址（URL）是不能随便更改的，只有站点地址（URL）可以随意动。如果更改了WordPress地址（URL），主页面可能就丢失了。

二、解决方案

1、使用ssh登录服务器

xshell等工具均可。

2、登录MySQL数据库

使用如下指令后，输入密码，打开mysql数据库：

mysql -u root -p

3、选中wordpress的数据库

USE wordpress;

4、查看wp_contens表单

select * from wp_options limit 1;


可以看到option_value这个属性值，如果WordPress地址（URL）修改错误，这个option_value就会变成那个错误的地址而无法再从后台更改，我们可以在数据库中对齐更改。

5、更改option_values

使用如下指令即可完成更改。your_wordpress_url为正确的WordPress地址（URL）。


UPDATE wp_options SET option_value="your_wordpress_url" WHERE option_name="siteurl";

更改完，就可以正常登陆主页了。

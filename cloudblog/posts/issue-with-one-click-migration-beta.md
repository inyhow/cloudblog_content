---
title: "Issue with One-click migration beta"
description: ""
category: ""
tags:
  -
status: published
reviewNote: ""
pinned: false
coverImage: ""
pubDate: 2026-03-18T12:07:31.380Z
updatedDate: 2026-03-18T12:07:31.380Z
scheduledAt: ""
affiliate: false
template: 
customData: {"price":"","affiliateLink":"","heroImage":""}
---

Please can someone help me. I need to fix this issue

> Failed: Site [naijawide.ng] failed to create, ERROR: An error was detected in the configuration file. Please solve it before proceeding

nginx: [emerg] open() "/www/server/panel/vhost/nginx/well-known/scholarship.naijawide.ng.conf" failed (2: No such file or directory) in /www/server/panel/vhost/nginx/scholarship.naijawide.ng.conf:11
nginx: configuration file /www/server/nginx/conf/nginx.conf test failed

* [aaPanel\_Kern](https://www.aapanel.com/forum/d/22169-issue-with-one-click-migration-beta/2) **replied to this.**

Hello, thank you for your feedback, this is a known issue
You can compress and download the /www/server/panel/vhost/nginx/well-known/ of the old server, upload it to the same directory of the new server and decompress it, and finally check whether the file is the same as the old server
and then migrate

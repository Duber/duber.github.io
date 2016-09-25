---
layout:     post
title:      "Disabling azure webjobs"
subtitle:   "How to completely stop web app's webjobs"
date:       2016-09-23 22:00:00
author:     "Start Bootstrap"
---

In Azure, if you want to prevent a web app's webjobs from running at any cost, you can add the following app setting to your website:

<blockquote>WEBJOBS_STOPPED = 1</blockquote>

Keep in mind that, otherwise, webjobs may run even when the app is stopped.

Where does this magic come from ? From kudu's documentation: [link](https://github.com/projectkudu/kudu/wiki/Web-Jobs){: target="_blank" }

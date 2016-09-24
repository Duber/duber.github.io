---
layout:     post
title:      "Disabling azure webjobs"
subtitle:   "How to completely stop web app's webjobs"
date:       2016-09-23 22:00:00
author:     "Start Bootstrap"
---

<p>In Azure, if you want to prevent a web app's webjobs from running at any cost, you can add the following app setting to your website:</p>

<blockquote>WEBJOBS_STOPPED => 1</blockquote>

<p>Keep in mind that, otherwise, webjobs may run even when the app is stopped.</p>

---
layout: post
title: "Start program automatically at startup in Windows"
date: 2014-02-22 11:19:20 +0700
categories: system_admin windows
tags: system_admin windows
---

There is an easy way to automatically start a program when Windows boots up. You don't have to write any script for it, just follow these 3 steps:

1. Create a shortcut for that program: **Right click** => choose **Create Shortcut**
2. Click **Start** => **All Programs** => right click folder **Startup** => choose **Open**

   If you couldn't find it, just paste the following link into **Windows Explorer**

   ```
   C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp
   ```

3. Paste the shortcut you just created in Step 1 into this folder

Alright, from now on, whenever you turn on or restart your machine, all programs inside this **Startup** folder will start automatically
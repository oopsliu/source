---
title: ArcGIS Python Addins
date: 2016-04-08 17:43:40
tags: [arcgis,python,desktop]
categories: Technology
---
![](http://i.stack.imgur.com/mOMaU.jpg)

Python addins经常显示[ Missing ]，比较崩溃，以下是常见原因：

1. 脚本中有中文等特殊字符（包括注释），但未设置适合的编码。可以尝试把中文改为英文，或在脚本首行加入编码类型，如# -*- coding: utf-8 -*-。 
2. 缩进格式不统一，有的地方是空格缩进，有的地方是Tab缩进。 
3. 文件路径中不能含有中文或空格。 
4. 系统环境变量的Path变量中没有Python27路径，如C:\Python27\ArcGIS10.4;C:\Python27\ArcGIS10.4\Scripts;C:\Python27\ArcGIS10.4\Lib。 
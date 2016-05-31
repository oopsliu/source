---
title: Hexo备忘录3 -- 多机同步
date: 2016-05-31 10:35:15
tags: [Hexo,git]
categories: Technology
---
公司和家里两台电脑的情况下（或者重装系统后）同步hexo的问题，经过亲测决定采用以下方式：

- node包和hexo等环境在两台机器上都手动配好（包括主题），不会经常变动；
- 经常更新的博客内容文件夹source放到github上托管，方便从不同机器上pull/push；
- hexo配置文件和主题配置文件不会经常更新，但是重新配置也有点麻烦，所以放到onedrive上备份，需要重新安装的时候可以直接使用；

试过整个hexo文件夹放到onedrive里，一是慢二是貌似posts的日期改了，所以评论都没有了。其他网盘基本都死掉了，百度云毫无理由的就是不！喜！欢！坚果云免费版流量太小，整体同步不够用，而且在准备开发者大会的时候出现了由于流量不够同步没成功，把ppt搞坏了！坑爹，果断删。

具体更新步骤怕忘记录一下：

1. 在hexo source下添加新文件后，hexo g, hexo d 
2. git add .
3. git commit -m "commit what了"
4. git push origin master到云端的repo上
5. 另一台机器同步的时候把云端的先pull下来，更新后再重复1-4提交到云端





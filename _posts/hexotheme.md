---
title: Hexo备忘录2 -- 主题theme
date: 2016-03-23 15:48:12
tags: [Hexo,theme,主题]
categories: Technology
---
对外协来说，内容什么的都是浮云，赶紧改个主题才是正经事！

# Clone Theme #
在官网上相中了Hueman主题，先用clone命令导到本地来：  
![](http://i.imgur.com/0LuC2Sw.png)

	git clone https://github.com/ppoffice/hexo-theme-hueman.git themes/hueman
在克隆过来的hueman文件夹里，把主题的配置文件_config.yml.example后缀example去掉，变成可用的config文件，然后修改Hexo整体的配置文件，即Hexo文件夹下的_config.yml，把theme项改成hueman:  

	# Extensions
	## Plugins: https://hexo.io/plugins/
	## Themes: https://hexo.io/themes/
	theme: hueman
执行hexo g, hexo s -p 5000在本地预览下，主题已经不是默认的landscape，而是Hueman主题了。

# 添加评论功能 #
Hueman主题默认的评论是Disqus，不知道是什么。。评论功能有三种选择，默认的Disqus，多说，和有言，虽然都没听说过是什么，但是看着多说比较顺眼，决定改成多说！去多说的官网（[http://duoshuo.com/](http://duoshuo.com/))注册个账号，然后创建站点，站点地址就填Hexo博客的地址，即http://oopsliu.github.io,再填一个多说域名，如http://oopsliu.duoshuo.com,创建成功后，将多说域名的前缀写入theme的配置文件里：  

	# Comment
	comment:
	    disqus: #hexo-theme-hueman # enter disqus shortname here
	    duoshuo: oopsliu
	    youyan: # enter youyan uid here

# 添加站内搜索 #
默认的搜索引擎是google，说多了都是泪，必须得换。。可以换成百度站内搜索，莫名的就不喜欢，只剩一个选择了，就是Swiftype。配置起来稍微有点麻烦，不过人家也是免费的，麻烦就麻烦点吧，配置参考步骤：
[http://www.jerryfu.net/post/search-engine-for-hexo-with-swiftype-v2.html](http://www.jerryfu.net/post/search-engine-for-hexo-with-swiftype-v2.html)
然后将Install Code填写到主题的配置文件里： 
 
	# Search
	search:
	    swiftype: v69sgvBSK3QqXXXXXXXX
	    baidu: false

# 其他配置 #
## 网站链接 ##
直接在配置文件里添加链接就行，但是要注意空格的问题：  

	# Miscellaneous
	miscellaneous:
	    open_graph: # see http://ogp.me
	        fb_app_id:
	        fb_admins:
	        twitter_id:
	        google_plus:
	    links:
	        ArcGIS知乎: http://zhihu.esrichina.com.cn/
	        Hexo: http://hexo.io

## About页面 ##
用 `$ hexo new page about` 会在source/about中生成index.md，然后在主题的配置文件里填写about页面的地址：  
	
	# Menus
	menu:
	    Home: /
	    # Delete this row if you don't want categories in your header nav bar
	    Categories:
	    About: /about/index.html

## 其他 ##
还改了几个配置项，比如网站logo、收藏夹图标favicon、主题颜色、分享至jiathis等等；另外修改/Hexo/scaffolds/post.md,添加上categories项，之后new出来的.md文件就都带分类了，Hueman主题会根据文章的分类自动给添加到导航栏上。


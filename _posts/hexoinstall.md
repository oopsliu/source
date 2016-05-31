---
title: Hexo备忘录1 -- 安装
date: 2016-03-22 10:58:06
tags: [Hexo,安装]
categories: Technology
---
# Cost #
Time：自己摸索1day左右，如果一切顺利，按照此memo应该1hour就ok了
Money：free

# 操作系统： #
办公室：win10
家里：win10

# 安装Git、Node.js #
1 安装Git后（https://www.git-scm.com/）,可以在右键菜单中看到Git Bash的选项：
![](http://i.imgur.com/yMnGbF5.png)

2 安装Node.js:
https://nodejs.org/en/download/

# 安装Hexo #
新建一个文件夹用来存放Hexo的文件们，第一次安装的时候放到了D盘上，后来发现如果想在多台电脑上发博客，比如办公室和家里两台电脑，就没法搞了，所以第二次直接把文件夹建到了OneDrive里。据说Dropbox的话同步时会生成其他文件，导致Hexo无法使用，未亲测。Anyway，放到OneDrive上貌似可行哦，虽然需要部署两次Hexo，而且同步文件可能会慢一些，但是我的需求也不会经常发博经常同步，所以应该可以满足了。

在OneDrive上新建一个文件夹HexoSync，然后在文件夹内右键Git Bash Here，在当前目录下执行安装命令：
    `$ npm install -g hexo-cli`

安装好后，再执行init命令生成各种静态文件：
    `$ hexo init`

成功后安装依赖包：
    `$ npm install`

安装好后执行`$ hexo g`重新生成静态文件：
![](http://i.imgur.com/h20EOyy.png)

然后把自己的电脑当做服务器，就可以在本地查看了。Hexo默认使用的端口是4000，和ArcGIS Server冲突，所以在使用本地服务器预览时得带个参数，把端口号改了：
    `$ hexo s -p 5000`

Git中显示本地服务器已启动后
![](http://i.imgur.com/F8cNrlj.png)，在浏览器中打开localhost:5000, 就可以看到最新的静态网页们，也就是最新的Hexo博客的样子了。

# 部署到GitHub上 #
部署在本地只能自嗨看看，要想让其他人也看到需要放到互联网能够访问到的服务器上。对域名有要求的可以花钱买个域名和服务器，没啥特殊要求的放在GitHub上托管我看就不错~

1 注册GitHub账号，新建一个repository，与自己的账户同名，比如我的github用户名是oopsliu，新建的repository就是oopsliu.github.io

2 修改Hexo文件夹（我的文件夹名为HexoSync）下的_config.yml文件，配置deploy项的设置：  

    `deploy:  
      type: git    
      repo: <repository url>    
      branch: [branch]      
      message: [message]`
如：  

    `deploy:
      type: git
      repo: https://github.com/oopsliu/oopsliu.github.io
      branch: master`

3 在HexoSync文件夹内运行Git Bash，安装github的部署工具： 

    `$ npm install hexo-deployer-git --save`

4 重新生成静态文件，并执行部署:  
 
    `$ hexo g
     $ hexo d`

5 git bash中显示部署成功 “Deploy done: git”后，稍等个一两分钟，等文件都同步完成，浏览器打开github上repo的url，如oopsliu.github.io，应该就可以看到部署好的博客了。

# 写博客 #
执行`$ hexo new articleName`就会在 HexoSync\source\_posts 文件夹下对应生成一个.md文件，可以直接使用markdown语法来编辑。删除了.md文件就是删除了该篇文章。试了几个markdown编辑器，马克飞象绑定Evernote，存取本地文件不方便，Cmd免费版的不能传本地图片，最后决定使用MarkDownPad。但是win10下html解析有问题，根据官网提供的解决方案安装了个Awesomium 1.6.6解决。代码段换行的问题目前觉得最好的方式是用空格空格回车开始代码段，然后整个代码段缩进一下就行。

# memo #
- 每次更改过配置后，都需要hexo g重新生成静态文件，再hexo s或hexo d部署到本地或github上查看；更改了文章的话不用重新generate，直接刷新就行

- 用notepad++编辑配置文件的时候，需要注意空格的问题，否则有可能读不到配置  

- 多个标签要用[]括起来，中间用逗号隔开


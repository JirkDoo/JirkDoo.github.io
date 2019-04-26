---
layout: page
title: 使用Jekyll和Github搭载博客
banner_image: /assets/images/2.jpg
tags: [Blog]
date:   2019-04-21
---

几天前心血来潮，决定搭建一个自己的博客。随便找了一些资料就入坑了，结果非常无奈的把所有坑都踩了一遍。

基本上分为以下几步：

- 本地调试
- Github的二级域名
- 绑定域名

本地调试是搭建博客中最为重要的一步。首先，安装 ruby，通过RubyGem 来安装Jekyll，一路下一步之后，安装完成，网上的博主说，安装完成以后会默认生成一个sites文件夹，反正我没找到，但是丝毫不影响我的操作，打开start command prompt with ruby and rails命令窗口执行

`gem install bundler`

接着执行

`gem install jekyll bundler`

这些操作结束以后，就可以着手来选择我们的需要的[博客模板](https://jekyll-themes.com/jekyll-theme-pdz/)了。

这个网站里面的模板比较新颖，符合追风少年风骚的审美，而且模板的简介里说明了他的功能，技术等方面，非常详细。但是注意！有些模板好像少了一些文件，我在第一次配置的时候，以为是ruby中的问题，配置很多遍都失败了，浪费了大量的精力。所以，这也是一门玄学。 在我们把主题下载下来以后，先备份一份再操作，这非常重要，下载到本地即可。

在start command prompt with ruby and rails命令窗口进入到你主题的文件夹，执行

`bundle exec jekyll serve`

如果你一遍通过，那么皆大欢喜。如果你遇到错误，那么一定要仔细的看提示错误的内容，你可以谷歌翻译，按照错误提示解决问题。本地调试的操作项基本完成。

至此，我们访问http://127.0.0.1:4000/  ，就会出现我们从Jekyll theme处下载的模板。

我们首先要明白Jekyll theme模板中的文件是做什么的，起到了什么作用：
```
.
├── _config.yml
├── _drafts
    ├── begin-with-the-crazy-ideas.textile
    └── on-simplicity-in-technology.markdown
├── _includes
    ├── footer.html
    └── header.html
├── _layouts
    ├── default.html
    └── post.html
├── _posts
    ├── 2019-04-17-something-start.md
    └── 2019-04-21-使用Jekyll+Github搭载博客.md
├── _site
├── .jekyll-metadata
└── index.html
```
我们可以参考[官方手册](http://jekyllcn.com/docs/structure/),这有里面比较重要的三个地方：

```
 _config.yml  //保存配置数据，在此修改原生主题的内容或结构
 _posts  //放置我们的文章，格式很重要，这里我使用markdown的文件格式
 _index.html  //是我们首页的入口
```

接下来我们在自己的github上新建一个公共仓库，仓库的名称填写

```
username.github.io  //这里的username是你自己的git名称
```

然后把这个仓库clone 到本地，把刚才配置好的文件全部复制到你的本地仓库中。再推到github上就好了。

搜索你设置的username.github.io，就可以出现你想要的网页了。

接下来是绑定域名，我在阿里云上购买的域名。我们在实名认证之后开始解析。

```
购买完，进入管理控制台 -> 云解析 -> 解析 -> 添加解析 -> 添加A记录 :
192.30.252.153
192.30.252.154
```

![JirkDoo](/pic/yuming.png)


在Jekyll theme文件中根目录下创建一个 **CNAME** 文件，在文件写你购买的域名，此处写的域名是裸域名，没有各种协议。

解析后我们搜索自己的域名，自己的博客就做好了。

但是Google显示这个不是安全的http，即没有ssl证书，这里我用cloudflare反向代理了一下。

大功告成。
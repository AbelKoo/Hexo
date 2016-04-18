---
title: Hexo+NexT+github搭建
date: 2016-04-18 13:55:55
tags: Hexo
---
本文介绍了使用Hexo+github搭建自己的静态博客的详细过程。
- 花了点时间，在github上搭建了自己的博客，既然完成了，那么老规矩发个教程作为首篇。
- 顺便使用了NexT主题，在搭建过程中有一些问题，我们逐一解决。


# 1 安装 #
- 在安装hexo之前，需要git以及nodejs
- 安装hexo（[hexo官网](https://hexo.io/)）


## 1.1 安装git ##
- Windows：下载并安装 [git](https://git-scm.com/download/win)。
- Mac：使用 [Homebrew](http://brew.sh/), [MacPorts](www.macports.org) 或 [安装程式](http://sourceforge.net/projects/git-osx-installer/) 安装。


## 1.2 安装Node.js ##
安裝 Node.js 的最佳方式通过[ nvm](https://github.com/creationix/nvm)。
cURL:
{% codeblock%}
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
{% endcodeblock%}
Wget:
{% code%}
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
{% endcode%}
一旦安裝完成，重啟終端機並執行下列指令以安裝 Node.js。
{%code%}
$ nvm install 4
{%endcode%}
或者您也可以下載 [安装程序](https://nodejs.org/en/) 來安裝。

## 1.3 安装hexo ##
安装完以上需求，就可以使用npm安装hexo
{% codeblock%}
$ npm install -g hexo-cli
{% endcodeblock %}

# 2 建站 #
## 2.1创建项目 ##
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
{%code%}
$ hexo init <folder>
$ cd <folder>
$ npm install
{%endcode%}

## 2.2项目结构 ##
创建完项目之后可以看到项目结构如下所示：
{%code%}
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
{%endcode%}
#### _config.yml ####
网站的 配置 信息，您可以在此配置大部分的参数。
#### package.json ####
应用程序的信息。EJS, Stylus 和 Markdown renderer 已默认安装，您可以自由移除。
#### scaffolds ####
模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。
#### source ####
资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。
#### themes ####
主题 文件夹。Hexo 会根据主题来生成静态页面。



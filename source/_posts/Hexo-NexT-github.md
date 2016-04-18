---
title: Hexo+NexT+github搭建
date: 2016-04-18 13:55:55
tags: Hexo
---
本文介绍了使用Hexo+github搭建自己的静态博客的详细过程。
- 花了点时间，在github上搭建了自己的博客，既然完成了，那么老规矩发个教程作为首篇。
- 顺便使用了NexT主题，在搭建过程中有一些问题，我们逐一解决。


# 安装 #
- 在安装hexo之前，需要git以及nodejs
- 安装hexo（[hexo官网](https://hexo.io/)）


## 安装git ##
- Windows：下载并安装 [git](https://git-scm.com/download/win)。
- Mac：使用 [Homebrew](http://brew.sh/), [MacPorts](www.macports.org) 或 [安装程式](http://sourceforge.net/projects/git-osx-installer/) 安装。


## 安装Node.js ##
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

## 安装hexo ##
安装完以上需求，就可以使用npm安装hexo
{% codeblock%}
$ npm install -g hexo-cli
{% endcodeblock %}

# 建站 #
## 创建项目 ##
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
{%code%}
$ hexo init <folder>
$ cd <folder>
$ npm install
{%endcode%}

## 项目结构 ##
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
### _config.yml ###
网站的 配置 信息，您可以在此配置大部分的参数。
### package.json ###
应用程序的信息。EJS, Stylus 和 Markdown renderer 已默认安装，您可以自由移除。
### scaffolds ###
模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。
### source ###
资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。
### themes ###
主题 文件夹。Hexo 会根据主题来生成静态页面。






# 运行 #
## 本地运行 ##
{%code%}
hexo server
{%endcode%}
执行成功后，可以通过localhost:4000进行访问。
## hexo常用命令 ##
{%code%}
hexo n     # new
hexo g     # generate
hexo s     # server
hexo d     # deploy
{%endcode%}



# 部署到github上 #
## github新建Repository ##
- 注意: 该仓库必须按照此格式命名: XXXX.github.io
- XXXX必须为你的github用户名（非邮箱等，不然搭建之后会有404）

## _config.yml ##
找到以下内容，并修改
{%code%}
deploy:
  type: git
  repository: git@github.com:XXXX/XXXX.github.io.git
  branch: master
{%endcode%}

- 5.0以上type为git，不在使用github，不然将找不到github。
- 使用ssh，而不是https

## 发布至github ##
{%code%}
hexo g
hexo d # 部署到github

Username for 'https://github.com':
hhstore   # 输入用户名

Password for 'https://XXXX@github.com':
XXXXX    # 提示输入用户密码.

INFO  Deploy done: git  # 提示部署成功.
{%endcode%}
- 若执行成功,会自动将public内容 同步到 hhstore.github.io 仓库.
- 若报错:ERROR Deployer not found: git , 执行如下命令:
{%code%}
npm install hexo-deployer-git --save
{%endcode%}
执行成功之后再执行一次：
{%code%}
hexo d
{%endcode%}


以上步骤无误，访问地址：XXXX.github.io



# 使用NexT #
主题：[NexT](http://notes.iissnan.com/)
## 下载NexT ##
{%code%}
cd your-hexo-site
git clone https://github.com/iissnan/hexo-theme-next themes/next
{%endcode%}
## 使用NexT ##
编辑_config.yml，找到以下内容：
{%code%}
theme: next
{%endcode%}
修改为NexT
## 更新 ##
{%code%}
hexo g
hexo d
{%endcode%}
成功之后打开博客地址
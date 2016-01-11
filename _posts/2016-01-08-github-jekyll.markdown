---
layout: post
title: "利用 GitHub 和 Jekyll 搭建个人博客"
---

---

目录

1. GitHub 和 Jekyll 简介
2. 环境搭建
    - 2.1 安装 Ruby 和 DevKit
    - 2.2 安装 Jekyll
3. 创建博客
4. 编写博客
5. 发布到 GitHub
    - 5.1 注册 GitHub 账号
    - 5.2 创建 SSH Key
    - 5.3 创建 GitHub 仓库
    - 5.4 创建 Git 仓库并推送
    - 5.5 创建 gh-pages 分支

---

### 1. GitHub 和 Jekyll 简介

####  **GitHub 是什么？**

> ###### GitHub 是一个用于存放 Git 版本控制系统所创建的仓库（repository）的网站。包括 Linux 的创始人 Linus Torvalds 在内的许多著名程序员都将代码开源并存放在 GitHub 上面。搭建个人博客网站使用 GitHub 提供的 GitHub Pages 服务。

> ###### *Github Pages 是面向用户、组织和项目开放的公共静态页面搭建托管服 务，站点可以被免费托管在 Github 上，你可以选择使用 Github Pages 默 认提供的域名 github.io 或者自定义域名来发布站点。Github Pages 支持 自动利用 Jekyll 生成站点，也同样支持纯 HTML 文档，将你的 Jekyll 站点托管在 Github Pages 上是一个不错的选择*

> ###### —— by[ Jekyllcn](http://jekyllcn.com/docs/github-pages/)

####  **Git 是什么？**

> ###### *Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。 Git的读音为/gɪt/。 Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。 Git 是Linus Torvalds 为了帮助管理Linux 内核开发而开发的一个开放源码的版本控制软件。*

> ###### —— by [百度百科](http://baike.baidu.com/subview/1531489/12032478.htm)

####  **Jekyll 是什么？**

> ###### *Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和我们的 Liquid 渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。*

> ###### —— by[ Jekyllcn](http://jekyllcn.com/docs/github-pages/)

---

### 2. 环境搭建

Jekyll 是 GitHub 创始人 Tom Preston-Werner 所编写的一套软件，这套软件是用 Ruby 编写的。因此，在安装 Jekyll 之前，需要先安装 Ruby 的运行环境。

#### 2.1 安装 Ruby 和 DevKit

要运行 Jekyll 至少需要下列软件：

- Ruby
- RubyGems
- DevKit

由于上面的软件中，DevKit 是最难安装的，本着写博客才是根本这个宗旨。所以要安装齐上面所有的软件，只需要简单的安装 [railsinstaller](http://railsinstaller.org/en) 就好了。 [railsinstaller](http://railsinstaller.org/en) 是 Ruby 的 Web 框架 Ruby on Rails 的一键安装套件，该套件包含了 Ruby、DevKit 和 Git 在内的 Jekyll 要用到的所有工具，不想折腾就简单安装就好了。

> **注意**：
> ###### 1. 在安装的过程中，记得将 `Install Git` 和 `Add executables for Ruby,DevKit and Git to the PATH` 这两个选项选中。
> ![Railsinstaller 选项](/assets/img/20160111/Railsinstaller-option.png)
> ###### 2. 在安装完成后，选中 `Configure git and ssh when installation has completed` 并点击 Finish，等待命令行运行完毕后再关闭命令行。
> ![Railsinstaller 配置](/assets/img/20160111/RailsInstaller-configure.png)

#### 2.2 安装 Jekyll

安装完成后，打开命令行界面（`win` + `r` 打开运行菜单，输入 `cmd` 运行）。

在命令行菜单中直接输入 `gem`，如果出现以下信息，就证明安装完成：

```
RubyGems is a sophisticated package manager for Ruby.  This is a
basic help message containing pointers to more information.
...
...
...
Further information:
   http://guides.rubygems.org
```

在命令行菜单中输入:

```
gem install jekyll
```

由于众所周知的原因，极有可能会出现以下错误信息：

```
Could not find a valid gem 'jekyll' (>= 0), here is why
...
```

这里的解决方案是在命令行菜单中输入以下命令（可能要翻墙）：

```
gem sources --remove https://rubygems.org/
gem sources -a http://rubygems.org/
gem install jekyll
```

然后等待一段时间，系统会自动安装所有需要的类。

安装完成后，可以在命令行中输入 `jekyll`，输出以下信息就证明安装成功：

```
A subcommand is required.
jekyll 3.0.1 -- Jekyll is a blog-aware, static site generator in Ruby
...
```

### 3. 创建博客

Jekyll 的用法非常简单，创建一个博客只需要在命令行（任意目录）下面简单的输入几行命令：

```
jekyll new myblog
cd myblog
```

上面 `jekyll new` 用于创建博客网站，`myblog` 表示要创建的博客的目录。如果需要在当前的目录直接创建博客，可以使用 `jekyll new .` 命令，`.` 代表当前目录。

创建完成后，`cd myblog` 用于在命令行中将当前的路径定位为 **myblog**。

Jekyll 内置了一个开发用的服务器，可以让你使用浏览器在本地浏览你的博客。需要在本地浏览器中浏览自己的博客，可以使用以下命令（在博客根目录）：

```
jekyll s
```

运行效果如下：

![myblog](/assets/img/20160111/myblog.png)

在启动服务器的过程中，有可能会遇到下列错误：

```
...
jekyll 3.0.1 | Error:  Permission denied - bind(2) for 127.0.0.1:4000
```

这是因为当前的电脑的端口 4000 被其他程序占用了，解决方法是打开目录下面的 **_config.yml** 文件，在最下方添加 `prot: 端口号`，其中端口号可以根据自己的需求而定，最好 10000 以上，但是不可以超过 65535。

![修改端口号](/assets/img/20160111/addport.png)

### 4. 编写博客

通过 `Jekyll new` 命令创建的博客，目录如下所示：

![博客目录](/assets/img/20160111/myblog-dir.png)

其中，目录 **_posts** 就是用来存放博客文件的，Jekyll 可以将 Markdown（或 Textile）、Liquid 和 HTML & CSS 构建可发布的静态网站。所有的博客文件都要符合下面的格式。

```
年-月-日-标题.MARKDOWN
```

如：

```
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.textile
```

只要符合 Jekyll 的命名规范，并将博客放在 **_posts** 文件夹中，这样运行就可以看到自己编写的博客了。

如我现在写的博客放在 **_posts** 中：

![放在 **_posts** 中](/assets/img/20160111/posts.png)

运行 Jekyll 自带的服务器就可以在浏览器中看到效果：

![浏览器中的效果](/assets/img/20160111/posts2.png)

### 5. 发布到 GitHub

通过上面的流程，只能让自己的博客运行在自己的电脑中，其他人是不可能看到的。因此，需要令所有人都可以看到我们的博客，还需要部署到网络上。

需要让我们的博客在网络上可以被浏览，我们需要一台服务器为我们服务。但是，服务器一般的人可消费不起，因此，我们可以借助 GitHub 提供的 Pages 服务。

#### 5.1 注册 GitHub 账号

GitHub 是一个网站，需要使用 GitHub 提供的服务，我们优先需要在 GitHub 上[注册账号](https://github.com/join)。

注册 GitHub 非常简单，只需要提供邮箱和密码等信息就可以快速的新建了，非常方便：

![注册 GitHub 账号](/assets/img/20160111/signin-github.png)

#### 5.2 创建 SSH Key

先检查在用户主目录下是否存在 .ssh 目录，如果有，在检查是否存在 **id_rsa** 和 **id_rsa.pub** 这两个文件，如果有，可以跳过这一步。

如果不存在，打开命令行界面并输入以下代码：

```
ssh-keygen -t rsa -C "youremail@example.com"
```

其中双引号中输入自己的邮箱。然后系统会提示安装路径和密码，这里没有特殊原因可以不设置密码。

安装完成后，登录 GitHub，并打开[设置菜单](https://github.com/settings/profile)。

![设置 SSH Key](/assets/img/20160111/sshkeys.png)

点击 **Add SSH key**，添加刚刚得到的公钥：

![添加公钥](/assets/img/20160111/addsshkey.png)

#### 5.3 创建 GitHub 仓库

在 GitHub 的首页中，找到新建仓库的选项：

![新建仓库](/assets/img/20160111/newrepository.png)

在创建仓库的信息中，填入仓库名为 yourname.github.io。
其中 yourname 是你的 GitHub 的用户名。

![创建仓库](/assets/img/20160111/create-repository.png)

创建完成后，会去到项目的主界面：

#### 5.4 创建 Git 仓库并推送

打开命令行，去到博客位置所在的根目录，输入以下命令：

```
git init
git add *
git commit -m "init jekyll"
```

其中：

```
# 初始化仓库
git init
# 添加当前目录所有文件到仓库
git add *
# 提交
git commit -m "init jekyll"
```

我们还需要将当前的仓库与远程仓库连接起来，因此还需要输入以下命令：

```
git remote add  origin git@github.com:ashkincode/ashkincode.github.io.git
```

然后，就可以将当前的博客推送到 GitHub 上（第一次推送要加上 -u）：

```
git push -u origin master
```

这时候应该就可以在 GitHub 中看到我们的代码：

![提交到远程仓库](/assets/img/20160111/gitpush.png)

#### 5.5 创建 gh-pages 分支

我们的目的是想在网络上直接访问 yourname.github.io 能够看到自己创建的网页。

但是，现在尝试一下访问自己的博客，你会发现无法访问。

这是因为 GitHub Pages 只会显示 gh-pages 分支上的内容。

因此我们还需要完后的步骤，在命令行中创建 gh-pages 分支：

```
git checkout -b gh-pages
```

将分支内容也推送到 GitHub：

```
git push origin gh-pages
```

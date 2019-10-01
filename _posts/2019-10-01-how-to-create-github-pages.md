---
layout: post
title: 如何创建自己的Github Pages
image_snippet: image_with_caption.html
---

Github Pages 是 Github 官方对于每一位用户提供的免费静态个人博客。你看的这篇文章就是使用 Github Page 写成的。

好处前面也提到了:

- **免费**，域名和服务器都由Github负责，不用自己掏钱维护服务器啦~
- **简单**，对于一个完全不懂网页前端的人也可以快速上手，使用现成的模板实现好看的UI
- **支持Markdown**，让编写博客不再费时费力
- **可扩展性强**，对于喜欢钻研的开发者，Github Page可以非常强大

当然缺点也是有的：

- **仅支持静态页面**，这意味着想实现一些网页请求是不可能的，最直观的就是无法直接实现评论系统（硬伤）[^1]
- **每个用户仅能发布一个站点**，并且站点的域名有固定的规则（一般是 _username_.github.io)

综合老说，Github Pages对非网页开发者还是友好的，尤其是没钱玩服务器的人（比如我）。Github 官方虽然有自己的 Github Pages 新手指南，但是实在是过于简洁，无法满足群众对于美的追求。所以这篇博文就根据我最近搭建博客踩到的坑总结一些经验。希望能给想要搭建自己博客又很迷茫的童鞋一些帮助~

## 1. 创建 Github Pages 专属仓库

Github Pages 需要一个专门的 Github 仓库来进行管理，这个仓库和你的其他仓库并无二致。不过有几个地方需要特别注意下：

- 仓库的命名格式是有特殊要求的，你必须将仓库命名为 _username_.github.io，其中 _username_ 是你的 Github 账号名
- 对于普通用户来说，这个仓库必须是公开的（记住开源精神啊魂淡~）

{% include image_with_caption.html src="/assets/images/create-repository.png" caption="创建仓库示例" %}

创建完成后我们需要使用 Git 将仓库克隆到本地，这样做有诸多裨益：

- 在本地编辑可以根据自己的喜好选择编辑器，增加工作效率
- 可以在本地搭建环境测试效果，这样即使在离线状态下也可以随心所欲地写博客啦

克隆指令可以使用 `git clone https://github.com/username/username.github.io` (注意替换 _username_ !! )

> 如果你还没有装 Git，这里友情提示 [官网](https://git-scm.com/) 链接，当然你也可以使用 [Github官方客户端](https://desktop.github.com/)。不过因为后续步骤中依然需要我们在本地安装 Git 环境，所以 Git 还是要提前安装好的。

## 2. 搭建本地运行环境

创建完仓库后，我们就可以通过自己喜欢的方式发布网页了。默认情况下 Github Pages 会寻找名为 `index.html` 的文件，并将其作为我们博客的主页。想要快速查看效果，你可以直接在克隆得到的本地仓库中新建一个 `index.html` 并写入 `Hello World` 进行测试。由于我们还没有搭建本地运行环境，所以你需要通过 `git commit/git push` 将新增的 `index.html` 文件同步到远程仓库中，再通过访问 `username.github.io` 查看效果。一切正常的话你会在自己的博客上看到 “Hello World” 的字样，象征着我们完成了搭建博客的第一步。但是如果只有如此苍白的文本，怎么能吸引别人来阅读我们的文章呢？所以我们还需要添加新的网页，新的 css 样式，新的 html 布局。。。——当然很多人在这一步就已经被劝退了。所以为了方便用户搭建自己的博客，Github Page 加入了对 Jekyll 的支持，从而大大简化了博客对于页面美观的需求，让我们可以将更多的精力花在写博文上。接下来的篇幅，将通过详细的步骤教会读者如何使用 Jekyll 实现一个美观实用的网站。

> 你可能会好奇 Jekyll 为何拥有化繁为简的魔力。其实这还是多亏了 Jekyll 能够将用户编写的 markdown 文件转换为对应的 html 文件。这样我们就可以通过调整不同 html 元素的 css 样式来实现统一的博文样式。这些 css 样式又以主题插件的形式打包在一起，所以即使用户不了解实现细节也可以很好地利用现成的主题打扮自己的网页。

### · 安装 Ruby

Jekyll 本质上属于一种 Ruby 语言的 Gem 包，可以类比为 Java 中的 Package。所以想要使用Jekyll，我们必须先在电脑上安装 Ruby 的运行环境。Windows 下可行的安装方法可以分为三种：

- 安装 Ubuntu(Linux) 虚拟机
- 使用 WSL(Windows Subsystem for Linux, 仅限win10最新版本)
- 使用 RubyInstaller

很巧这三种我都试过了，最后发现如果只用 Jekyll 的话，还是第三种最简单。~~想要了解 Linux 系统的童鞋可以尝试下 WSL，我试了下发现可能会因为用户权限问题导致下载时卡住，所以就没有用了~~ 这里直接给出 RubyInstaller 的[官方下载地址](https://rubyinstaller.org/downloads/)，安装非常方便，全程下一步就可以了。

在进行下个步骤前首先得了解一下什么是Gem。Gem 是 Ruby 模块 (也可以称为 Gems) 的包管理器。使用 Gem 指令安装 Ruby 模块就和 Ubuntu 下的apt-get, Python 的 pip 一样简单，我们只需要在命令行中敲一行代码，就可以等待 Gem 帮我们执行所有剩下的步骤了。最新版的 Ruby 中已经自带有 Gem 了，所以我们只需要打开命令行，输入以下指令就可以安装Bundler：

```bash
gem install bundler
```

如果你发现自己的下载速度奇慢无比的话，可以尝试将 Gem 的下载地址替换为国内镜像，需要的指令也非常简单：

```bash
$ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
$ gem sources -l
https://gems.ruby-china.com
# 确保只有 gems.ruby-china.com
```

由于我们还需要使用 bundler，所以还需要设置 bundler 的镜像下载网站

```bash
bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

### · 安装 Github Pages 依赖包

那么 Bundler 到底是做什么的呢？简单来说，使用它是为了更好地维护我们博客的依赖关系。试想下面这种情况，我们的博客使用到了除 Jekyll 外的其他 Gem 插件，而其他的插件明确要求必须使用 `Jekyll 2.1` 版本，如果你刚好在电脑中安装了该版本，那么事情可能会很简单。但是如果你需要借鉴别人的博客写法，他的博客因为年代比较久远，只能在 `Jekyll 1.5` 版本下正常运行，又该怎么处理呢？ Bundler 正是为了应付这种情况而准备的。相比于只在系统全局中安装某一个版本的 Gem，我们还可以选择在每个仓库中维护一份单独的 Gem 依赖关系。这样不同的项目之间就不会发生相互干扰的问题了。

> 我看到的大部分教程中都将 Bundler 和 Jekyll 的安装合在一起，但是实际上这样并不是很妥当。为了防止因为不同 Gem 插件之前版本不一致引发的一系列问题，我们完全可以使用 Bundler 为每个仓库安装单独的运行环境。这样不仅方便我们自己使用，也方便和其他人分享。

进入本地仓库目录，并修改仓库的本地配置，使仓库中所有用到的 gems 都安装到我们指定的位置:

```bash
$ bundle config --local path vendor/bundle
# 将本地仓库的 gems 安装位置修改为 vendor/bundle
$ bundle config
# 使用该命令确定修改是否生效
path
Set for your local app (F:/xxx/.bundle/config): "vendor/bundle"
```

使用 `bundle init` 指令进行初始化，这样会在仓库根目录下生成一个 `Gemfile` 文件，安装依赖包时 bundler 会根据该文件中的配置执行。修改 `Gemfile` 中的内容如下:

```gemfile
source "https://rubygems.org"  # 下载 Gems 的地址

gem "github-pages" # 指定安装 Github Pages 依赖包
```

最后执行 `bundle install` 即可，耐心等待 bundler 将所有依赖关系处理好吧~

> 还有一种可选方法是直接安装 Jekyll (`gem "jekyll"`)，区别在于安装 Github Pages 时一样会安装 Jekyll，并且会附带把 Github Pages 直接支持的几种主题也安装到本地。这样就可以像Github Setting 中一样，只需要改动一行代码，便能浏览不同主题下博客的效果。

### · 运行本地服务器进行测试

现在我们可以直接在本地测试博客的显示效果了，执行 `bundle exec jekyll serve`，然后在浏览器中打开 `http://127.0.0.1:4000`。 恭喜你，你现在可以在本地修改博客并预览效果啦。当然，这条指令会持续执行，并可以实时反映你所做的修改。如果想要关闭本地服务器，只需要在命令行中按下 `Ctrl + C` 即可。

## 扩展阅读

- [Github Pages 官方介绍](https://pages.github.com/)
- [Jekyll 官方文档](https://jekyllrb.com/docs/)
- [RubyGems - Ruby China](https://gems.ruby-china.com/)

---
[^1]: 当然我们可以通过一些折衷的方式来实现，其中比较出名的应该是[gitment](https://github.com/imsun/gitment)

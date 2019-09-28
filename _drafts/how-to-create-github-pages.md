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

### · 安装 Ruby

### · 安装 Bundler 并配置

### · 安装 Jekyll 并配置

### · 运行本地服务器进行测试

## 3. 编写第一条博客

## 4. 推送

## 扩展阅读

[Github Pages 官方介绍](https://pages.github.com/)

---
[^1]: 当然我们可以通过一些折衷的方式来实现，其中比较出名的应该是[gitment](https://github.com/imsun/gitment)

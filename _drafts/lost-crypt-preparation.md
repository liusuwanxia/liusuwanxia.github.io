---
layout: post
title: 《Lost Crypt》学习笔记（1）——部署游戏项目
image_snippet: image_with_caption.html
---
最近准备开一个新坑，学习一下 Unity 最新推出的2D游戏解决方案。为了演示自家的引擎有多强大，Unity 现身说法，直接放出了一个几乎涵盖所有新技术的游戏 Demo《Lost Crypt》。由于工作上使用的一直是旧版的Unity，对于Unity近一年的发展几乎是鲜有关注了。所以当我打开Unity 2019.3 时确实被震撼到了，索性重操旧业，写一写学习心得，希望能对几个月后的自己有点帮助(ಥ _ ಥ)。之前写Blog，都是一次性写完，费时又费力，所以这次干脆分段落写，希望能多坚持一段时间吧。。

## 1. 安装Unity Hub及最新版Unity

Unity Hub 是 Unity 公司为了方便管理各种版本的Unity发行的一个启动器，现在还兼具了社区和学习的功能，不论是初学者还是资深开发者都很值得使用。还没有用过的可以到官网对应的 [下载页面][] 下载。由于《Lost Crypt》现在还属于测试阶段，所以我们只能在 Unity 2019.3 及以上版本学习它，直奔主题安装（话说这个Unity Hub安装速度比以前直接安快了不是一点啊。。）

![安装2019](/assets/images/install-unity-2019-3.gif)

## 2. 添加资源

接下来我们需要从 Asset Store 上下载《Lost Crypt》的资源。在之前的工作流程里，想要把一个Asset 添加到我们需要的项目里是一件很繁琐的事情。然而通过 Unity 2019.3 中改进过的 **Package Manager**，我们就能很轻松地完成:

- 在 Asset Store 里找到 [Lost Crypt][] 并添加到我的资源
- 打开 Package Manager，切换到 **My Asset** 标签页并找到对应的资源包（这一步需要联网并登录自己的Unity账户！！！）
- 点击导入资源后静静地等待

## 3. 查看学习向导

没错，这个Demo里甚至还自备了学习向导，帮助你梳理各种 2D 功能并辅以快速跳转的指引。不出意外的话我可能就会按照这个向导里的顺序来写作了。正常情况下你每次打开项目都会自动弹出该向导，但你也可以在任何时候双击 `Assets/DiscoverWindow/DiscoverLostCrypt.asset` 打开该窗口。

[下载页面]: https://store.unity.com/download?ref=personal
[Lost Crypt]: https://assetstore.unity.com/packages/essentials/tutorial-projects/lost-crypt-2d-sample-project-158673

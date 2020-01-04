---
layout: post
title: 《Lost Crypt》学习笔记（2）——PSD Importer
image_snippet: image_with_caption.html
---
2D PSD Importer 是一个专门用于将 Photoshop  生成的 PSB 文件导入 Unity 的工具包。 它可以基于原始的 PSB 文件生成一个由 Sprite 组成的 Prefab，从而省去了在 Unity 重新组合 Sprite 的繁琐工作。

> 这里的 PSB 文件并不是 PSD 文件的错误拼写，而是一种单独的文件格式（可以理解为 "PSD BIG"），它和 PSD 文件的功能完全相同，并且支持更大分辨率的图片。

## 1. PSD Importer 是如何提高工作效率的

在没有该工具包前，Unity虽然可以处理 PSD 文件，但是却并不会解析其中的图层信息，所以比较普遍的做法是手动将不同的图层平铺开来，再使用 **Sprite Editor** 中的切图工具切割。这样我们想要把美术设置的人物搬到游戏里就需要如下的步骤：

1. 美术画出由不同图层（通常一个图层代表一个身体部位）组成的角色完成图
2. 美术将叠在一起的图层手动平铺开，并放在同一张图片中组成部件平铺图
3. 程序收到美术的角色完成图和部件平铺图，将平铺图片的 **Texture Type** 设置为 **Multiple** 并进行切割，得到若干部位的 Sprite 资源
4. 程序按照角色完成图将所有部件按照固定的层级关系组装起来，构成一个拥有许多 **Sprite Renderer** 的 Prefab。

{% include image_with_caption.html src="/assets/images/2D-workflow.jpg" caption="2D人物制作" %}

而使用了 PSD Importer后，我们省去了 2，3，4 的步骤。PSD Importer 可以帮助我们从美术递交的角色完成图中生成部件平铺图，并且按照 PSD 中的层级关系构建出完整的 Prefab，效率可谓是大大提高了。

## 2. 安装 PSD Importer 资源包

如果你已经在本地部署好了《Lost Crypt》的项目，那么恭喜你，PSD Importer 作为依赖项已经被自动添加到项目中了。你同样可以通过 Package Manager 检查或安装该工具包。成功安装后，当你将 psb 后缀的文件添加到 Unity 中时，Unity 会自动调用 PSD Importer 接管导入过程，你只需要点击 psb 文件，并在 Inspector 窗口中进行简单的设置即可。

## 3. 导入设置解析

相比于普通的图片导入， PSB 文件的导入设置中要多了不少新花样，本节将对它们逐个解析。

{% include image_with_caption.html src="/assets/images/psd-importer-inspector.png" caption="导入设置一览" %}

- `Import Hidden`: 是否导入隐藏图层。用过PS的人应该都知道，一个 PSB 文件是由很多个不同的图层叠加在一起组成的，这和 Unity 中 UI 的组织方式有点像。默认情况下 PSB 文件中的隐藏图层是不会被处理的，勾选该选项将一视同仁，对 PSB 中的所有图层都进行处理。

- `Mosaic`: 仅当 **Texture Type** 被设置为 **Multiple** 时该选项才会出现。勾选该选项将会根据 PSB 文件中的图层信息自动生成部件平铺图和分割好的 Sprite 资源。（对应于第一节中提到的步骤2,3）

- `Character Rig`: 勾选该设置会根据 PSB 文件自动生成 Prefab， Prefab 中的层级关系和 PSB 文件中的图层关系基本一致。 （对应于第一节中提到的步骤4）

- `Use Layer Grouping`：仅当勾选 **Character Rig** 后该选项才可用。自动生成的 Prefab 将会根据 PSB 文件的图层组进一步细化子节点的结构，建议勾选。

- `Pivot`: 设置自动生成的 Prefab 的轴点。这项设置会影响 Prefab 旋转时的表现。

- `Reslice`: 勾选该设置会在生成部件平铺图时废弃所有之前在该图片文件上的改动（例如手动切分的子Sprite）。

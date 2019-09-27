---
layout: post
title: 为 Github Pages 设置字体
image_snippet: image_with_caption.html
---
Github Pages 支持的几种主题里使用的字体种类和大小都有所区别，但是通常都不能满足我们的实际需要。毕竟用于展示的主题中仅用到了英文字符，对于中文没有很好的支持。为了达到更好的阅读效果，我们可以定制适合自己的网页字体。

## l. 创建自定义样式表

从原理上来说，Github Pages 的页面样式就源自于基本的css样式，所以我们设置网页的字体，直接在css样式中修改就可以了。为了不破坏 Github Pages 主题内置的样式，我们可以在根目录下创建新的 `assets\css` 目录用于存放我们自定义的网页样式。 首先创建一个名为 `style.scss` 的文件, 在开头加入以下代码：

```css
---
---

@import "{{ site.theme }}";
```

{{ site.theme }} 表示主题自带的样式文件，通过导入该文件，我们就相当于继承了所有主题默认的样式， 随后我们就可以添加自己想要的样式了，这样即使与默认的样式发生了冲突，也会判定我们添加的新样式生效。

## 2. 添加希望使用的字体文件

下载自己希望使用的字体 **ttf** 文件，然后将其添加到 `assets\fonts` 目录下。为了方便在样式表中引用它，我们可以先在样式表中添加对应的 `fontface`：

```css
@font-face {
    font-family: "MSYH";
    src: url("/assets/fonts/MSYH.ttf");
}
```

这里通过`font-face`, 定义了一种可以在随后的样式中访问的名为 `MSYH` 的 `font-family`， 当样式表读到这种`font-family`时，就会到`src`指定的位置去找对应的字体。 当然这里的命名和使用的ttf文件都应该根据你选择的字体而进行改变。我这里选择使用微软雅黑字体来显示汉字，所以将其命名为 “MSYH”（_Microsoft YaHei_)。字体的文件名最好手动改为英文，以防止因为一些编码问题导致的错误。

## 3. 设置字体类型和大小

现在就可以使用我们定义好的 `font-family` 来设置应用于所有页面的字体了！首先在之前创建的 `style.scss` 中继续添加下面的代码：

```css
body {
    font-family: "Times New Roman", "MSKT";  
    font-size: 20px;  
}
```

首先是字体类型的设置，`font-family`用于指定希望使用的字体类型。我们可以同时指定多种字体。这样当渲染文本时就会按照从左到右的顺序依次查找字体类型是否可用，如果当前字体类型不包含想要渲染的文字，就会交给下一种字体类型处理。我们这里同时指定两种字体是有深层含义的，**目的是对于英文和中文使用不同的字体**。之所以这样做，是因为虽然我使用的**微软雅黑**对于中文显示良好，但是对于英文就显得比较难看了。所以我将一种纯英文字体 **Times New Roman** 放在中文字体前面，当渲染英文时会优先使用该字体，当渲染中文时由于没有对应的字体可用，就会使用第二优先级的 **微软雅黑** 字体。这样无论是中文还是英文，都可以得到很好的展示了。
> 你可能会好奇我们没有添加 **Times New Roman**，为何就可以直接使用了。这是因为该字体实在太过常用，所以 Github Pages 已经内置了。

其次字体大小`font-size`的设置就比较简单了，完全可以按照自己的喜好调节，我这里使用的是20px。

## 4. 检查字体是否生效

经过上面的三个步骤，你的网页字体应该成功得到修改了，如果效果不是很明显，可以通过**chrome**等浏览器自带的**检查**功能进行核实。

{% include image_with_caption.html src="/assets/images/font-setting-inspect.png" caption="检查html组件的css样式" %}

从下图中可以明显看出文本已经成功设置为指定的字体类型:
{% include image_with_caption.html src="/assets/images/font-setting-font-confirm.png" caption="font-family设置成功" %}

## 扩展阅读

- 如果对于本文提到的 css 样式想要进一步的了解，可以查询 [W3schools.com](https://www.w3schools.com/cssref/css3_pr_font-face_rule.asp) 。
- 关于如何在本地搭建Jekyll网站并进行测试，可以参考 [Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)

> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [forum.obsidian.md](https://forum.obsidian.md/t/generate-custom-pdfs-with-pandoc-panrun-and-the-eisvogel-latex-template/22237/16) ![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/shadekingcam/90/33755_2.png)最初发表在我的[博客在这里 334](https://shadeking.cam/blog/obsidian-slick-pdf-report/). 检查所有链接（这是我的第一篇文章，所以我仅限于 5 个链接）

目标
--

我想重复地将 markdown 转换为时尚的自定义 pdf。我用 markdown 来记下我所有的笔记，感谢我对黑曜石的不朽热爱。特别是对于我即将到来的 OSCP 考试重考，我希望能够快速流畅地将我的笔记从黑曜石中取出，变成一份看起来很专业的报告，我可以为上交而感到自豪。

我对完成的定义是这样的：

*   降价输入生成 PDF 输出
*   我可以控制足够的风格来使其成为我自己的风格
    *   代码块应具有语法突出显示
    *   我可以使用我从未完成的颜色和资源[投资组合网站 158](https://shadeking.cam)
    *   **很高兴拥有**：样式在降价_中_控制以影响输出 PDF，从而更轻松地创建模板
*   我可以轻松地在其他报告中重用该样式
*   该过程应该易于编写脚本

工具
--

*   潘多克
*   潘润
*   [艾斯福格尔乳胶模板 363](https://github.com/Wandmalfarbe/pandoc-latex-template)
*   GIMP 为标题页和后续页面制作背景图像

风格
--

我绝不是设计师，但我相信我正在用我的[投资组合网站 158](https://shadeking.cam). 网站上的颜色很大程度上受到星际飞船提示的启发，尤其是洋红色，我稍微修改了一下，到处都使用，以及我在 fontjoy 中偶然发现的字体。我真的很喜欢立交桥单声道标题的技术外观，所以我很想在我的报告中使用这些标题。

我的目的是创建一个我打算多次使用的模板，并且我希望使用该模板的报表具有美感。有了这个，以及 Eisvogel LaTex 模板允许您为页面背景和标题页背景设置变量的事实，我开始在 Gimp 中创建这些背景，这些背景是链接文档中页面上的背景，并在下一节中链接为和。`titlepage-background: "TitlePageBackground.png"``page-background: "PageBackground.png"`

使用 Panrun 和 Eisvogel 模板
-----------------------

Panrun 是一个工具，允许您在 markdown 文档的 yaml 前言中为 pandoc 设置参数，因此您不必记住必须传递的所有参数。我的前言最终看起来像这样：

```
---
note_type: reference
writing_type: draft
title: Academy.htb
author: 5hade
titlepage: true
titlepage-rule-color: "ff0d8a"
titlepage-background: "TitlePageBackground.png"
titlepage-text-color: "eaecef"
page-background: "PageBackground.png"
colorlinks: "ff0d8a"
toc: true
toc-own-page: true
mainfont: DejaVuSerif
sansfont: Overpass Mono
linkcolor: magenta
urlcolor: magenta
listings-no-page-break: true
code-block-font-size: \scriptsize
output:
  pdf:
    pdf-engine: xelatex
    output: academy-htb.pdf
    from: markdown
    template: eisvogel
    listings: true
---
```

前两个 yaml 物品不是用于 panrun，而是我在黑曜石金库中使用的前品。块中的那些由 pandoc 使用，其余的都由 Eisvogel 模板直接用于设置 PDF 输出的样式和格式。`output`

重用模板
----

现在我已经完成了一次，我可以创建一个模板，以便在我想输出另一个报表时使用。我使用[模板程序 92](https://silentvoid13.github.io/Templater/docs) 我的模板看起来像这样：

```
---
note_type: <% tp.system.suggester(["thought", "media", "transient", "plan", "meeting", "presentation", "reference", "draft"], ["thought", "media", "transient", "plan", "meeting", "presentation", "reference", "draft"]) %>
writing_type: draft
title: <% tp.file.cursor(1) %>
author: <% tp.file.cursor(2) %>
titlepage: true
titlepage-rule-color: "ff0d8a"
titlepage-background: "<% tp.user.home_dir() %>/Pictures/pandoc/TitlePageBackground.png"
titlepage-text-color: "eaecef"
page-background: "<% tp.user.home_dir() %>/Pictures/pandoc/PageBackground.png"
colorlinks: "ff0d8a"
toc: true
toc-own-page: true
mainfont: DejaVuSerif
sansfont: Overpass Mono
linkcolor: magenta
urlcolor: magenta
listings-no-page-break: true
code-block-font-size: \scriptsize
output:
  pdf:
    pdf-engine: xelatex
    output: <%tp.file.title%>.pdf
    from: markdown
    template: eisvogel
    listings: true
---
```

结果！
---

以下是制作本文档的结果，以及我用来测试系统的退役 HackTheBox 机器的文章。

![](https://forum.obsidian.md/uploads/default/optimized/3X/2/3/23ae2740ee7407f406071bd10df1a79b31271aa7_2_394x499.png) ![](https://forum.obsidian.md/uploads/default/optimized/3X/6/a/6af8b8d379aeb625d0d05f4871ac2489f6c38088_2_353x500.png) ![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/den/90/1932_2.png)

令人 印象 深刻！令人 印象 深刻

![](https://forum.obsidian.md/images/emoji/apple/wave.png?v=9)

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/moonbase59/90/13648_2.png)

现在_这_具有真正的价值！非常感谢您的分享！

（终于有人使用 YAML _以_正确的方式设置 Pandoc 和 LaTeX 参数了！

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/kenanmike/90/18316_2.png)

好东西！  
你用什么来实际将 md 笔记导出到 Latex 等？

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/shadekingcam/90/33755_2.png)

哦，我实际上从来没有将文档导出到乳胶。乳胶模板是我在 github 上找到的，它提供了我发现非常有用的选项。对我来说，在所有 yaml 就位的情况下，我实际上要做的就是 ，它将使用 yaml 标头中设置的选项运行 pandoc。在模板中，它们设置为：`panrun <filename>.md`

```
pdf:
    pdf-engine: xelatex
    output: <%tp.file.title%>.pdf
    from: markdown
    template: eisvogel
    listings: true
```

其运行方式与 Eisvogel 是模板从 GitHub 下载到我的 ~/.pandoc/templates 目录相同`pandoc --pdf-engine xelatex -o <filename>.md -f markdown --template eisvogel --listings`

![](https://forum.obsidian.md/letter_avatar_proxy/v4/letter/m/e495f1/90.png)

你对泛润的替代品有什么想法吗？

*   似乎必须为此安装红宝石很麻烦
*   我已经安装了它，但似乎仍然无法正常运行

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/shadekingcam/90/33755_2.png)

我在我的包管理器中根本没有看到任何替代方案。查看源代码 （[潘润 / 盘润在师傅 ·MB21 / 潘润 ·GitHub 27](https://github.com/mb21/panrun/blob/master/panrun)） 它只有 185 行 Ruby，可能可以很容易地移植到 Python 或任何对你的用例有意义的东西中。

![](https://forum.obsidian.md/letter_avatar_proxy/v4/letter/m/e495f1/90.png)

我的想法完全一样，我将尝试在 python 中创建一个并行

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/kenanmike/90/18316_2.png)

如果您成功了，如果您同意，请在此线程中发布代码！

![](https://forum.obsidian.md/letter_avatar_proxy/v4/letter/m/e495f1/90.png)

计划是在 github 上放一些东西。可能需要一点时间，但一旦我有了它就会发回这里。

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/pseudometa/90/17551_2.png)

仅供参考：我认为您甚至可以简化一下，因为 Pandoc 现在拥有[用于从 YAML 文件读取元数据的选项 59](https://pandoc.org/MANUAL.html#option--defaults) 跟。所以基本上，你不需要 panrun。`--defaults=FILE`

尽管如此，工作流程还是不错的

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/shadekingcam/90/33755_2.png)

哦！这很整洁，我没见过。有了这个，你不会失去使用模板器附带的替换的能力吗？我阅读文档中该部分的方式，看起来这看起来像是寻找一个独立的 yaml 文件，而不是能够读取降价前言中的 yaml。也许我对此的理解是不正确的。我认为 panrun 的目的是能够在每个文档的基础上更改内容，例如，如果您想更改文件名，或者如果您为不同的报告有不同的标题页。

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/shadekingcam/90/33755_2.png)

如果您也在寻找一个，我很乐意做出贡献！不反对红宝石，但我更喜欢我所有的工具 python！

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/pseudometa/90/17551_2.png)

我认为你是对的。据我所知，有一个 [Pandoc 开发人员之间正在进行的讨论是否将所有信息包含在一个文件中 48](https://github.com/jgm/pandoc/issues/5870).

![](https://forum.obsidian.md/letter_avatar_proxy/v4/letter/m/bbce88/90.png)

您好，我看到了您的消息，所以我创建了一个基于 panrun 的 python 脚本

![](https://forum.obsidian.md/images/emoji/apple/smile.png?v=10)

![](https://github.githubassets.com/favicons/favicon.svg) [GitHub](https://github.com/mjcc30/panrun)

![](https://forum.obsidian.md/uploads/default/optimized/3X/4/3/43735a7cf30ee6dc7c6456c513bbd356186a6aa1_2_690x345.png)

### [GitHub - mjcc30/panrun：在降价中查看 YAML 元数据的脚本... 89](https://github.com/mjcc30/panrun)

在降价文件中查看 YAML 元数据并为您运行 pandoc 的脚本。- GitHub - mjcc30/panrun：在降价文件中查看 YAML 元数据并为您运行 pandoc 的脚本。

我是 python 的新手，所以你可以让它变得更好

![](https://forum.obsidian.md/user_avatar/forum.obsidian.md/digitecture/90/33011_2.png)

![](https://forum.obsidian.md/uploads/default/optimized/3X/d/c/dc45d65ac81441fea865cd6807ead3aaabd32d44_2_690x446.jpeg)

经过大量工作，我已经能够完成 Pandoc 模板格式设置，以根据先前在 CLS 中使用 LaTex 模板的工作进行改进。

我发现默认的 Pandoc 模板需要文档将其制作成其他人可以轻松修改的东西，因为它可以从 LaTex 包运行，然后定义元素以将其移动到通常在适当的排版文档中找到的东西。

基于这些发现，我认为现在考虑转向黑曜石和降价是有意义的，这些文档不需要在 Latex 中编写脚本的强度，以便通过 Pandoc 和良好的模板处理格式。

还有其他人对此任务感兴趣吗？
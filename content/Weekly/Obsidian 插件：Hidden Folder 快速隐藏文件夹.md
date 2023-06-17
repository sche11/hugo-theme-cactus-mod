> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [pkmer.cn](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/hidden-folder-obsidian/)

> Pkmer，一个发掘无限潜力，共享知识管理的社区！这个开源社区为您提供最新最全的知识管理工具、技巧和经验分享，助您创造更高效、更智慧的知识管理体系。让我们一起开启无限可能！

> *   插件名称：Hidden Folder
> *   插件版本：1.0.7
> *   插件作者：ptrsvltns
> *   插件描述：快速隐藏文件夹
> *   插件项目地址：[点我跳转](https://github.com/ptrsvltns/hidden-folder-obsidian)

效果 & 特性
-------

*   通过正则表达式来隐藏 Obsidian 文件管理器中的目录 / 文件夹

使用
--

*   需要使用插件自带的设置，来完成设定。
*   首先，书写好正则表达式，定义你要隐藏的文件夹
*   其次，开启选项，选择是隐藏这些文件夹，还是恢复已经隐藏的文件夹 ![](https://cdn.pkmer.cn/images/20230616211439.png!pkmer)

### 一些简单正则表示方式

*   隐藏文件夹

```
- folder1 <- match
  - folder1
  - folder2
- folder2
  - folder1
  - folder2
```

*   匹配文件中文件名内容

```
- folder1
  - folder1
    - subabcfolder1 <- match
  - folderabc2 <- match
- folder2
  - foldabcer1 <- match
  - folder2abc <- match
```

*   匹配

```
- folder1
  - folder1
  - folder2
- folder2
  - folder1 <- match
  - folder2
```

```
- folder1 <- match
  - folder1
  - folder2
- folder2
  - folder1 <- match
  - folder2
```

```
- folder1
  - folder1 <- match
  - folder2
- folder2
  - folder1
  - folder2
```
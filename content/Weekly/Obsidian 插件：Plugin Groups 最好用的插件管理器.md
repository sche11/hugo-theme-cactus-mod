> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [pkmer.cn](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/obsidian-plugin-groups/)

> Obsidian 插件：Plugin Groups 最好用的插件管理器

概述
--

Obsidian 是一个简洁而又功能强大的笔记应用，吸引了许多用户。社区有许多插件可供选择，使你可以根据自己的需求定制工作流程和体验。有如此多的插件可供选择，有时候很容易迷失在插件的海洋中，不知道该从何处开始尝试。久而久之插件的数量就会增长起来，进而启动速度会变慢（请问你装 10 个、20 个、30 个？），插件之间因为一些原因也可能长生互相冲突和干扰。

幸运的是，Plugin Groups 就是一款管理插件的插件，可以帮助我们更好地组织和管理我们的插件。以及有时候面对不同工作模式，或者工作流分支的时候，我们想要关闭一些插件，让 Obsidian 更纯粹。

> **插件名片**
> 
> *   插件名称：Plugin Groups
> *   插件版本：2.1.0
> *   插件作者：Mocca101
> *   插件描述：帮你轻松地分组和管理 Obsidian 第三方插件，启动关闭，加载插件
> *   插件项目地址：[点我跳转](https://github.com/Mocca101/obsidian-plugin-groups)

效果 & 特性
-------

![](https://cdn.pkmer.cn/images/20230616203115.png!pkmer)

*   **分组：** 将 Obsidian 的插件进行编组，以便于后续批量管理
*   **批量操作：** 通过单击或命令启用或禁用组中的插件
*   **延迟组加载：** 自定义延迟后加载
*   **组嵌套：** 使用嵌套组管理。

使用
--

### 创建分组

*   自定义分组，插件允许你自定义分组，分组的名称
*   选择后续的新安装插件，是否加入到次分组
*   是否在 Obsidian 启动时间记载这个组
*   为该组设置一个快捷键，可以快速开启 / 关闭该组的插件

![](https://cdn.pkmer.cn/images/20230616205644.png!pkmer)

![](https://cdn.pkmer.cn/images/20230616205134.png!pkmer)

### 编辑分组

要编辑一个已存在的组，请在插件设置中点击组名旁边的铅笔图标。从这里，你可以像创建组那样编辑组。另外，你还可以从设置中的插件列表中选择插件应属于哪些组。

### 开启 / 关闭分组

你可以通过在插件设置中的组名旁边点击 “On” 和 “Off” 按钮来启用或禁用一个组。如果启用了组，你也可以在命令面板中使用以下命令来启用或禁用你的组：

*   插件组启用：” 你的组名称 ”
*   插件组禁用：” 你的组名称 ”

### 延迟启动

*   使用组的 General -> Startup 功能
*   Load on Startup：设置是否在开启时启动
*   Delay：设置启动延迟时间，最低 0s，最大 25s

这个方法可以打打提升一些在启动阶段不需要马上使用的插件。从而加速 OB 的启动速度。

> **建议**
> 
> *   遗憾的是，目前还不能设置插件组内启动插件的顺序。因此，如果插件之间存在依赖关系，并且某个插件需要在另一个插件之前加载，我建议将它们放在不同的组中，并相应地加载这些组。尽管可能在不这样做的情况下也能运行，但我建议为了安全起见不要这样做。

兼容和适配
-----

有些插件不能使用延迟加载，因为它们需要在工作区加载之前加载。下面是已知的列表：

*   [pane-relief](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/pane-relief)
*   [hidden-folder-obsidian](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/hidden-folder-obsidian)

一些插件也会有一些小问题（没有加载正确的视图）。这可以通过关闭并重新打开受影响的窗格来解决。例如：

*   Media Extended

有时窗格会自动重新加载，但这只会发生在插件加载后，例如：

*   [obsidian-kanban](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/obsidian-kanban)
*   [obsidian-outliner](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/obsidian-outliner)

如果你注意到某个插件存在延迟加载的问题，请告诉插件作者，或则在插件项目地址的 README.md 文件中添加插件到列表中并提交 PR。
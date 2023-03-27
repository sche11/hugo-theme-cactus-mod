> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [github.com](https://github.com/joethei/obsidian-rss)

> Read RSS Feeds from inside obsidian. Contribute to joethei/obsidian-rss development by creating an ac......从黑曜石内部阅读 RSS 提要。通过创建一个 ac...

[](#rss-reader)RSS Reader  [](#rss-reader)RSS 阅读器
-------------------------------------------------

Plugin for [Obsidian](https://obsidian.md) 黑曜石插件

[](#)[![](https://camo.githubusercontent.com/ba14264398cfea46b0f650a8006fbe55e310e4912a8cbdae533d6ac0dd21904c/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f7061636b6167652d6a736f6e2f762f6a6f65746865692f6f6273696469616e2d727373)](https://camo.githubusercontent.com/ba14264398cfea46b0f650a8006fbe55e310e4912a8cbdae533d6ac0dd21904c/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f7061636b6167652d6a736f6e2f762f6a6f65746865692f6f6273696469616e2d727373) [![](https://camo.githubusercontent.com/7d519fd9742299967f80e7748659c8c23921b085e166c879137fc1a54f9cbd21/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6d616e69666573742d6a736f6e2f6d696e41707056657273696f6e2f6a6f65746865692f6f6273696469616e2d7273733f6c6162656c3d6c6f77657374253230737570706f7274656425323061707025323076657273696f6e)](https://camo.githubusercontent.com/7d519fd9742299967f80e7748659c8c23921b085e166c879137fc1a54f9cbd21/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6d616e69666573742d6a736f6e2f6d696e41707056657273696f6e2f6a6f65746865692f6f6273696469616e2d7273733f6c6162656c3d6c6f77657374253230737570706f7274656425323061707025323076657273696f6e) [![](https://camo.githubusercontent.com/6261185cff6076523eb467209965e980a37da50b5d9277ea6817a20334c59602/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f6a6f65746865692f6f6273696469616e2d727373)](https://camo.githubusercontent.com/6261185cff6076523eb467209965e980a37da50b5d9277ea6817a20334c59602/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f6a6f65746865692f6f6273696469616e2d727373) [![](https://camo.githubusercontent.com/380d9de715ed958cdd2879a1bb08d8c15cd77b1c2369eae76e778499dd539bdd/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6c69626572612d6d616e69666573746f2d6c69676874677265792e737667)](https://liberamanifesto.com)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

![](https://camo.githubusercontent.com/9d4133fe9383c32112b4cdba73779406ee64790fc360f1107e4fe8c2a0351c87/68747470733a2f2f692e6a6f65746865692e73706163652f6f6273696469616e2d7273732e706e67)

[](#features)Features  [](#features)功能
--------------------------------------

*   Reading RSS feeds from within obsidian  
    从黑曜石内部读取 RSS 提要
*   Sorting feeds into folders 将源分类到文件夹中
*   staring articles 凝视文章
*   creating new notes from articles 从文章创建新笔记
*   pasting article into current note  
    将文章粘贴到当前笔记中
*   creating custom filters 创建自定义筛选器
*   tagging articles 标记文章
*   support for audio and video feeds  
    支持音频和视频源
*   reading articles with Text to speech (if the [TTS plugin](https://github.com/joethei/obsidian-tts) is installed)  
    阅读带有文本转语音的文章（如果安装了 TTS 插件）
*   multi language support(see [#43](https://github.com/joethei/obsidian-rss/issues/43) for translation instructions)  
    多语言支持（有关翻译说明，请参见 [#43](https://github.com/joethei/obsidian-rss/issues/43) ）
*   and more on the [Roadmap](https://github.com/joethei/obsidian-rss/projects/1)  
    以及有关路线图的更多信息

![](https://camo.githubusercontent.com/a0b12693f3d1e0a521d5cb73ff0bdd831d620bb3aacbc6ebc7d0a9e5678ff3e8/68747470733a2f2f692e6a6f65746865692e73706163652f515141545775333665432e676966) [ ![](https://camo.githubusercontent.com/a0b12693f3d1e0a521d5cb73ff0bdd831d620bb3aacbc6ebc7d0a9e5678ff3e8/68747470733a2f2f692e6a6f65746865692e73706163652f515141545775333665432e676966) ](https://camo.githubusercontent.com/a0b12693f3d1e0a521d5cb73ff0bdd831d620bb3aacbc6ebc7d0a9e5678ff3e8/68747470733a2f2f692e6a6f65746865692e73706163652f515141545775333665432e676966)   [](https://camo.githubusercontent.com/a0b12693f3d1e0a521d5cb73ff0bdd831d620bb3aacbc6ebc7d0a9e5678ff3e8/68747470733a2f2f692e6a6f65746865692e73706163652f515141545775333665432e676966) 

[](#getting-started)Getting Started  [](#getting-started)入门
-----------------------------------------------------------

After installing the plugin: 安装插件后：

*   Go to the plugin configuration and add a feed (under the _Content_ section).  
    转到插件配置并添加源（在“内容”部分下）。
*   In Obsidian, expand the right hand pane and click the RSS tab.  
    在黑曜石中，展开右侧窗格并单击 RSS 选项卡。

[](#finding-the-rss-feed-for-a-website)Finding the RSS feed for a website  
[](#finding-the-rss-feed-for-a-website)查找网站的 RSS 提要
-------------------------------------------------------------------------------------------------------------------------------

*   Search for the RSS logo or a link on the website  
    在网站上搜索 RSS 徽标或链接
*   Use an browser addon ([Firefox](https://addons.mozilla.org/en-US/firefox/addon/awesome-rss/), [Chrome based](https://chrome.google.com/webstore/detail/get-rss-feed-url/kfghpdldaipanmkhfpdcjglncmilendn))  
    使用浏览器插件（火狐，基于Chrome）
*   Search the websites sourcecode for `rss`  
    在网站源代码中搜索 `rss`

[](#tips)Tips  [](#tips)提示
--------------------------

*   get fulltext content for some truncated RSS feeds with [morss.it](https://morss.it/)  
    获取一些截断的 RSS 源的全文内容 morss.it
*   get feeds from some social media sites with [RSS Box](https://rssbox.herokuapp.com/)  
    使用RSS Box从某些社交媒体网站获取提要
*   Filter content from feeds with [SiftRSS](https://siftrss.com/)  
    使用 SiftRSS 过滤提要中的内容
*   Get an RSS feed for a site that does not support RSS with [RSS-proxy](https://github.com/damoeb/rss-proxy/) or [RSS Hub](https://github.com/DIYgod/RSSHub)  
    获取不支持带有 RSS 代理或 RSS 集线器的 RSS 的网站的 RSS 源

[](#template-variables)Template variables  [](#template-variables)模板变量
----------------------------------------------------------------------

*   `{{title}}` title of article  
    `{{title}}` 文章标题
*   `{{link}}` link to article  
    `{{link}}` 文章链接
*   `{{author}}` author of article  
    `{{author}}` 文章作者
*   `{{published}}` publishing date, you can also specify a custom date format like this: `{{published:YYYYMMDD}}`  
    `{{published}}` 发布日期，您还可以指定自定义日期格式，如下所示： `{{published:YYYYMMDD}}`
*   `{{created}}` date of note creation, you can also specify a custom date format like this: `{{created:YYYYMMDD}}`  
    `{{created}}` 笔记创建日期，您还可以指定自定义日期格式，如下所示： `{{created:YYYYMMDD}}`
*   `{{content}}` the actual content  
    `{{content}}` 实际内容
*   `{{description}}` short description  `{{description}}` 简短说明
*   `{{folder}}` the folder the feed is in  
    `{{folder}}` 提要所在的文件夹
*   `{{feed}}` the name of the feed  
    `{{feed}}` 提要的名称
*   `{{filename}}` the filename, only available in the new file template  
    `{{filename}}` 文件名，仅在新文件模板中可用
*   `{{tags}}` - tags, seperated by comma, you can also specify a seperator like this: `{{tags:;}}`  
    `{{tags}}` - 标签，用逗号分隔，您也可以像这样指定一个分隔符： `{{tags:;}}`
*   `{{#tags}}` - tags with #, seperated by comma, with #, you can also specify a seperator like this: `{{#tags:;}}`  
    `{{#tags}}` - 带有#的标签，用逗号分隔，用#分隔，您还可以指定这样的分隔符： `{{#tags:;}}`
*   `{{media}}` link to media  
    `{{media}}` 链接到媒体
*   `{{highlights}}` - list of highlights, you can also specify a custom style, this example creates a [admonition](https://github.com/valentine195/obsidian-admonition) for each highlight:  
    `{{highlights}}` - 突出显示列表，您还可以指定自定义样式，此示例为每个突出显示创建一个告诫：![](https://camo.githubusercontent.com/ff7524bef87ef4dd6ab1806fc2b42cb60caa8a3e32425868b30d6fc58f66ca98/68747470733a2f2f692e6a6f65746865692e73706163652f6f6273696469616e2d7273732d686967686c696768742d73796e7461782e706e67)

[](#-security)⚠ Security  [](#-security)⚠ 安全
--------------------------------------------

*   This plugin contacts the servers that host the RSS feeds you have specified.  
    此插件联系托管您指定的 RSS 源的服务器。
*   RSS feeds can contain arbitrary data, this data will get sanitized before being displayed.  
    RSS 源可以包含任意数据，这些数据将在显示之前进行清理。
*   Many Obsidian plugins use codeblocks to add some functionality. This plugin sanitizes these codeblocks at read/note creation time. This is to block rss feeds from executing arbitrary plugin code.  
    许多黑曜石插件使用代码块来添加一些功能。此插件在读取/注释创建时清理这些代码块。这是为了阻止 rss 提要执行任意插件代码。
*   Some plugins allow for different kinds of inline syntax's, these are treated individually (Currently only _Dataview_ and _Templater_).  
    一些插件允许不同类型的内联语法，这些语法是单独处理的（目前只有Dataview和Templater）。

[](#styling)Styling  [](#styling)样式
-----------------------------------

If you want to style the plugin differently you can use the following css classes  
如果你想以不同的方式设置插件的样式，你可以使用以下 css 类

*   rss-read RSS-read
*   rss-not-read RSS 不读
*   rss-filters RSS 过滤器
*   rss-folders RSS 文件夹
*   rss-folder rss 文件夹
*   rss-feed RSS-提要
*   rss-feed-title
*   rss-feed-items
*   rss-feed-item
*   rss-tag RSS-tag
*   rss-tooltip
*   rss-modal
*   rss-title RSS-title
*   rss-subtitle RSS-字幕
*   rss-content RSS 内容

For help with styling you can also check out the `#appearance` channel on the [Obsidian Members Group Discord](https://obsidian.md/community)  
有关样式的帮助，您还可以查看黑曜石成员组 Discord 上的 `#appearance` 频道

### [](#installing-the-plugin)Installing the plugin  [](#installing-the-plugin)安装插件

*   `Settings > Third-party plugins > Community Plugins > Browse` and search for `RSS Reader`  
    `Settings > Third-party plugins > Community Plugins > Browse` 并搜索 `RSS Reader`
*   Using the [Beta Reviewers Auto-update Tester](https://github.com/TfTHacker/obsidian42-brat) plugin with the repo path: `joethei/obsidian-rss`  
    使用带有存储库路径的 Beta 审阅者自动更新测试器插件： `joethei/obsidian-rss`
*   Copy over `main.js`, `styles.css`, `manifest.json` from the releases to your vault `VaultFolder/.obsidian/plugins/rss-reader/`.  
    将 `main.js` 、 `styles.css` 、 `manifest.json` 从版本复制到保管库 `VaultFolder/.obsidian/plugins/rss-reader/` 。
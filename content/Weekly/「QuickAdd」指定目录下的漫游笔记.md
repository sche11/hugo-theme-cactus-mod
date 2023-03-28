> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [forum-zh.obsidian.md](https://forum-zh.obsidian.md/t/topic/1163/5) ![](https://forum-zh.obsidian.md/user_avatar/forum-zh.obsidian.md/borber/90/266_2.png)

指定目录下的漫游笔记
==========

准备工作
----

*   `Templater` 插件
*   `QuickAdd` 插件
*   "世上无难事, 只要肯放弃" 的良好心态

安装
--

0.  将下方 `js` 代码保存到你的 `Templater`脚本目录 请将 "产出", "卡片" 改为你自己的目录地址

```
module.exports = random
let quickAddApi;
let folders = ["产出", "卡片"]

async function random (params) {
    ({quickAddApi} = params) 
    let notes = app.fileManager.vault.fileMap[folders[Math.floor(Math.random() * folders.length)]].children
    let note = notes[Math.floor(Math.random() * notes.length)].path
    await app.workspace.activeLeaf.openFile( await app.vault.getAbstractFileByPath(note) );
}
```

命名推荐为: `folderRandom.js`

1.  创建一个新的 `QuickAdd` 宏 命名建议 `folderRandom` 添加之前保存的 js 函数  
    
    ![](https://forum-zh.obsidian.md/uploads/default/optimized/1X/c2f9838ea0cc80c9656e90b3cb44def8dc6ab254_2_520x500.png)
    
2.  添加一个 `Capture` 设置如下:  
    
    ![](https://forum-zh.obsidian.md/uploads/default/optimized/1X/26fc8286f75823f837ae08b67bd4a394b01e997c_2_543x500.png)
    
    所用文本: `{{MACRO:folderRandom::random}}`
    
3.  尽情享用吧
    

祝你生活愉快
------

![](https://forum-zh.obsidian.md/letter_avatar_proxy/v4/letter/c/7cd45c/90.png)

分享一个能实现类似功能的 ob 插件 smart random note

![](https://github.githubassets.com/favicons/favicon.svg) [GitHub](https://github.com/erichalldev/obsidian-smart-random-note)

![](https://forum-zh.obsidian.md/uploads/default/optimized/1X/005fc8bf438222db1fcd6195975b7a880954be96_2_690x345.png)

### [GitHub - erichalldev/obsidian-smart-random-note: A smart random note plugin... 25](https://github.com/erichalldev/obsidian-smart-random-note)

A smart random note plugin for Obsidian. Contribute to erichalldev/obsidian-smart-random-note development by creating an account on GitHub.

用 Quickadd 比较极客，如果不太熟悉，可以用已有插件

搜索语句：  
path:-“More/100-![:green_book:](https://forum-zh.obsidian.md/images/emoji/twitter/green_book.png?v=10 ":green_book:") 日志”

表示排除 文件夹 “More/100-![:green_book:](https://forum-zh.obsidian.md/images/emoji/twitter/green_book.png?v=10 ":green_book:") 日志”。
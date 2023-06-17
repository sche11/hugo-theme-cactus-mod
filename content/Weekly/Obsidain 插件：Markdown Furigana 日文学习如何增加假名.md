> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [pkmer.cn](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/obsidian-markdown-furigana/)

> Obsidain 插件：Markdown Furigana 日文学习如何增加假名

学习日文时经常需要知道汉字的发音（假名），Markdown Furigana 插件可以很方便的输入与显示振假名（振り反名／ふりがな），同时也能处理注音符号与汉语拚音。  

> **插件名片**
> 
> *   插件名称：Markdown Furigana
> *   插件作者：Steven Kraft
> *   插件说明：日语书写中给对应的汉字生成注音假名
> *   插件项目地址：[点我跳转](https://github.com/steven-kraft/obsidian-markdown-furigana)

语法
--

{汉字 | かんじ}，{汉字 | ㄏㄢ ˋ| ㄗ ˋ}，{汉字 | han|zi}

{地球 | ほし} {汉 | おとこ} {强敌 | とも} {本気 | マジ} {凝视 | みつめ} る

![](https://cdn.pkmer.cn/images/7507a79e4a47f4178e9b57e126ac5c4f_MD5.png!pkmer)

1.  {汉字 | ㄏㄢ ˋ ㄗ ˋ}： {汉字 | ㄏㄢ ˋ ㄗ ˋ}

```
<ruby>汉字<rt>ㄏㄢˋㄗˋ</rt></ruby>
```

1.  {汉字 | ㄏㄢ ˋ| ㄗ ˋ}：{汉字 | ㄏㄢ ˋ| ㄗ ˋ}

```
<ruby>汉<rt>ㄏㄢˋ</rt>字<rt>ㄗˋ</rt></ruby>
```

![](https://cdn.pkmer.cn/images/5ab1ca163822e3dd4fb2695d5762f43b_MD5.png!pkmer)

扩展阅读
----

HTML 标签 ruby

> 旁注标记（ruby character），或称注音标示、加注音、Ruby 字元、ruby 或 rubi，是一种表意文字的音标印刷方式，广泛地运用于日文及中文。一般这些字是放于表意文字的上方或右边，作为文字的拼音或注释。

### 样式 ruby-position

#### 注音样式在上

```
<ruby  style="ruby-position:over">汉字<rt>ㄏㄢˋ ㄗˋ</rt></ruby>
```

#### 注音样式在下

```
<ruby  style="ruby-position:under">汉字 <rt>ㄏㄢˋㄗˋ </rt></ruby>
```
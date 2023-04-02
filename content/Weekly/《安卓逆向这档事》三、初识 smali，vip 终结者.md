> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.52pojie.cn](https://www.52pojie.cn/thread-1701353-1-1.html)

> [md]# 一、课程目标 ---1. 了解 JVM、Dalvik、ART2. 初识 smali 语法 3. 实战修改 smali# 二、工具 ---1. 教程 Demo(更新)2.MT 管理器 / NP 管理器 3. 雷电模拟 ... 《......

一、课程目标

* * *

1. 了解 JVM、Dalvik、ART  
2. 初识 smali 语法  
3. 实战修改 smali

二、工具
====

* * *

1. 教程 Demo(更新)  
2.MT 管理器 / NP 管理器  
3. 雷电模拟器  
4.jadx-gui  
5. 核心破解

三、课程内容
======

* * *

1. 什么是 JVM、Dalvik、ART
---------------------

JVM 是 JAVA 虚拟机，运行 JAVA 字节码程序  
Dalvik 是 Google 专门为 Android 设计的一个虚拟机，Dalvik 有专属的文件执行格式 dex(Dalvik executable)  
Art(Android Runtime) 相当于 Dalvik 的升级版，本质与 Dalvik 无异

2.smali 及其语法
------------

smali 是 Dalvik 的寄存器语言，smali 代码是 dex 反编译而来的。

关键字

<table><thead><tr><th>名称</th><th>注释</th></tr></thead><tbody><tr><td>.class</td><td>类名</td></tr><tr><td>.super</td><td>父类名，继承的上级类名名称</td></tr><tr><td>.source</td><td>源名</td></tr><tr><td>.field</td><td>变量</td></tr><tr><td>.method</td><td>方法名</td></tr><tr><td>.register</td><td>寄存器</td></tr><tr><td>.end method</td><td>方法名的结束</td></tr><tr><td>public</td><td>公有</td></tr><tr><td>protected</td><td>半公开，只有同一家人才能用</td></tr><tr><td>private</td><td>私有，只能自己使用</td></tr><tr><td>.parameter</td><td>方法参数</td></tr><tr><td>.prologue</td><td>方法开始</td></tr><tr><td>.line xxx</td><td>位于第 xxx 行</td></tr></tbody></table>

数据类型对应

<table><thead><tr><th>smali 类型</th><th>java 类型</th><th>注释</th></tr></thead><tbody><tr><td>V</td><td>void</td><td>无返回值</td></tr><tr><td>Z</td><td>boolean</td><td>布尔值类型，返回 0 或 1</td></tr><tr><td>B</td><td>byte</td><td>字节类型，返回字节</td></tr><tr><td>S</td><td>short</td><td>短整数类型，返回数字</td></tr><tr><td>C</td><td>char</td><td>字符类型，返回字符</td></tr><tr><td>I</td><td>int</td><td>整数类型，返回数字</td></tr><tr><td>J</td><td>long （64 位 需要 2 个寄存器存储）</td><td>长整数类型，返回数字</td></tr><tr><td>F</td><td>float</td><td>单浮点类型，返回数字</td></tr><tr><td>D</td><td>double （64 位 需要 2 个寄存器存储）</td><td>双浮点类型，返回数字</td></tr><tr><td>string</td><td>String</td><td>文本类型，返回字符串</td></tr><tr><td>Lxxx/xxx/xxx</td><td>object</td><td>对象类型，返回对象</td></tr></tbody></table>

常用指令

<table><thead><tr><th>关键字</th><th>注释</th></tr></thead><tbody><tr><td>const</td><td>重写整数属性，真假属性内容，只能是数字类型</td></tr><tr><td>const-string</td><td>重写字符串内容</td></tr><tr><td>const-wide</td><td>重写长整数类型，多用于修改到期时间。</td></tr><tr><td>return</td><td>返回指令</td></tr><tr><td>if-eq</td><td>全称 equal(a=b)，比较寄存器 ab 内容，相同则跳</td></tr><tr><td>if-ne</td><td>全称 not equal(a!=b)，ab 内容不相同则跳</td></tr><tr><td>if-eqz</td><td>全称 equal zero(a=0)，z 即是 0 的标记，a 等于 0 则跳</td></tr><tr><td>if-nez</td><td>全称 not equal zero(a!=0)，a 不等于 0 则跳</td></tr><tr><td>if-ge</td><td>全称 greater equal(a&gt;=b)，a 大于或等于则跳</td></tr><tr><td>if-le</td><td>全称 little equal(a&lt;=b)，a 小于或等于则跳</td></tr><tr><td>goto</td><td>强制跳到指定位置</td></tr><tr><td>switch</td><td>分支跳转，一般会有多个分支线，并根据指令跳转到适当位置</td></tr><tr><td>iget</td><td>获取寄存器数据</td></tr></tbody></table>

其余指令可用语法工具查询

定位方法：搜索弹窗关键字、抓取按钮 id

例子：

```
//一个私有、静态、不可变的方法   方法名
.method private static final onCreate$lambda-2(Lkotlin/jvm/internal/Ref$IntRef;Lcom/zj/wuaipojie/ui/ChallengeSecond;Landroid/widget/ImageView;Landroid/widget/ImageView;Landroid/widget/ImageView;Landroid/view/View;)Z //(这里面是方法的参数)这里是方法返回值类型，表示布尔值类型，返回假或真
    .registers 7  //寄存器数量

    .line 33  //代码所在的行数
    iget p0, p0, Lkotlin/jvm/internal/Ref$IntRef;->element:I  //读取p0(第一个参数，参考寄存器知识)中element的值赋值给p0

    const/4 p5, 0x1  //p5赋值1

    const/16 v0, 0xa //v0赋值10，在16进制里a表示10

    if-ge p0, v0, :cond_15  //判断p0的值是否大于或等于v0的值(即p0的值是否大于或等于10)，如果大于或等于则跳转到:cond_15

    .line 34  //以下是常见的Toast弹窗代码
    check-cast p1, Landroid/content/Context; //检查Context对象引用

    const-string p0, "请先获取10个硬币哦" //弹窗文本信息，把""里的字符串数据赋值给p0

    check-cast p0, Ljava/lang/CharSequence; //检查CharSequence对象引用

    invoke-static {p1, p0, p5}, Landroid/widget/Toast;->makeText(Landroid/content/Context;Ljava/lang/CharSequence;I)Landroid/widget/Toast; 
    //将弹窗文本、显示时间等信息传给p1

    move-result-object p0  //结果传递给p0

    invoke-virtual {p0}, Landroid/widget/Toast;->show()V  //当看到这个Toast;->show你就应该反应过来这里是弹窗代码

    goto :goto_31  //跳转到:goto_31

    :cond_15 //跳转的一个地址

    invoke-virtual {p1}, Lcom/zj/wuaipojie/ui/ChallengeSecond;->isvip()Z  //判断isvip方法的返回值是否为真(即结果是否为1)

    move-result p0  //结果赋值给p0

    if-eqz p0, :cond_43 //如果结果为0则跳转cond_43地址

    const p0, 0x7f0d0018  //在arsc中的id索引，这个值可以进行查询

    .line 37
    invoke-virtual {p2, p0}, Landroid/widget/ImageView;->setImageResource(I)V //设置图片资源

    const p0, 0x7f0d0008

    .line 38
    invoke-virtual {p3, p0}, Landroid/widget/ImageView;->setImageResource(I)V

    const p0, 0x7f0d000a

    .line 39
    invoke-virtual {p4, p0}, Landroid/widget/ImageView;->setImageResource(I)V

    .line 40
    sget-object p0, Lcom/zj/wuaipojie/util/SPUtils;->INSTANCE:Lcom/zj/wuaipojie/util/SPUtils; 

    check-cast p1, Landroid/content/Context;

    const/4 p2, 0x2 //p2赋值2

    const-string p3, "level" //sp的索引

    invoke-virtual {p0, p1, p3, p2}, Lcom/zj/wuaipojie/util/SPUtils;->saveInt(Landroid/content/Context;Ljava/lang/String;I)V //写入数据

    goto :goto_50 //跳转地址

    :cond_43

    check-cast p1, Landroid/content/Context;

    const-string p0, "\u8bf7\u5148\u5145\u503c\u5927\u4f1a\u5458\u54e6\uff01" //请先充值大会员哦！

    check-cast p0, Ljava/lang/CharSequence;

    invoke-static {p1, p0, p5}, Landroid/widget/Toast;->makeText(Landroid/content/Context;Ljava/lang/CharSequence;I)Landroid/widget/Toast;

    move-result-object p0

    invoke-virtual {p0}, Landroid/widget/Toast;->show()V

    :goto_50
    return p5  //返回p5的值
.end method //方法结束

//判断是否是大会员的方法
.method public final isvip()Z
    .registers 2

    const/4 v0, 0x0 //v0赋值0

    return v0 //返回v0的值

.end method
```

修改方法：修改判断、强制跳转、修改寄存器的值

![](https://attach.52pojie.cn/forum/202212/29/105642ke3zpmf6lkxeeijr.png)

**Carnac 汉化版_104NufeJ3A.png** _(18.6 KB, 下载次数: 1)_

[下载附件](forum.php?mod=attachment&aid=MjU4MTg4OHxlNWRhZjkxOHwxNjgwNDQyNTI4fDE0ODI3Nzd8MTcwMTM1Mw%3D%3D&nothumb=yes)

2022-12-29 10:56 上传

3. 寄存器
------

在 smali 里的所有操作都必须经过寄存器来进行: 本地寄存器用 v 开头数字结尾的符号来表示，如 v0、 v1、v2。 参数寄存器则使用 p 开头数字结尾的符号来表示，如 p0、p1、p2。特别注意的是，p0 不一定是函数中的第一个参数，在非 static 函数中，p0 代指 “this"，p1 表示函数的第一个 参数，p2 代表函数中的第二个参数。而在 static 函数中 p0 才对应第一个参数 (因为 Java 的 static 方法中没有 this 方法）

四、课后小作业
=======

* * *

1. 关掉视频自己复现三种方法  
2. 完成这个作业 demo(因为最近实在是太太太忙了，绝对不是因为我懒，咕咕咕。搞懂这个 demo 那也基本上能理解本节课的内容)  
丑小鸭师傅的 demo  
链接：[https://pan.baidu.com/s/1cUInoi](https://pan.baidu.com/s/1cUInoi) 密码：07p9  
原文链接：[教我兄弟学 Android 逆向 02 破解第一个 Android 程序](https://www.52pojie.cn/thread-650395-1-1.html)

五、反思 & 答疑
=========

* * *

关于 jadx 搜不到大会员的 unicode 编码，这是因为我录视频之前在设置里把 unicode 的转义打开而导致的，像你们第一次安装 jadx 都是默认关闭这个选项的，所以能直接搜到大会员的汉字！！！

由于准备不是很充足，我感觉我讲的不是太好，多看看我列举参考文档有利于理解 smali 语法。

对于开发者而言，在打包应用时，最好对代码进行混淆，否则逆向人员轻而易举得进行 Crack，或者说在写代码的时候就不要用 isvip、getvip 等易辨识的单词作为方法名

待更新

六、视频及课件地址
=========

* * *

[百度云](https://pan.baidu.com/s/1cFWTLn14jeWfpXxlx3syYw?pwd=nqu9)  
[阿里云](https://www.aliyundrive.com/s/TJoKMK6du6x)  
PS：阿里云在维护，暂时看不到第三课内容  
[哔哩哔哩](https://www.bilibili.com/video/BV1wT411N7sV)

PS: 解压密码都是 52pj，阿里云由于不能分享压缩包，所以下载 exe 文件，双击自解压

七、其他章节
======

* * *

[《安卓逆向这档事》一、模拟器环境搭建](https://www.52pojie.cn/thread-1695141-1-1.html)  
[《安卓逆向这档事》二、初识 APK 文件结构、双开、汉化、基础修改](https://www.52pojie.cn/thread-1695796-1-1.html)  
[《安卓逆向这档事》四、恭喜你获得广告 & 弹窗静默卡](https://www.52pojie.cn/thread-1706691-1-1.html)

八、参考文档
======

* * *

[吾爱破解安卓逆向入门教程（三）--- 深入 Smali 文件](https://www.52pojie.cn/thread-396966-1-1.html)  
[吾爱破解安卓逆向入门教程（四）---Smali 函数分析](https://www.52pojie.cn/thread-397858-1-1.html)  
[【原木文章】Android 改造者之路 - 02. 初探 smali 功法](https://www.52pojie.cn/thread-1485681-1-1.html)
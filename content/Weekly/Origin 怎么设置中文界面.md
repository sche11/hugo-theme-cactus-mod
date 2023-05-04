> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/600534106)

Origin 是由 OriginLab 公司开发的一个科学绘图、数据分析软件。该软件操作简单易学，在科研界很受欢迎，但是正版 Origin 安装后是英文界面如下图：

![](https://pic3.zhimg.com/v2-6d9e13abf7e733d92615312c3d02474e_r.jpg)

虽然作为科研人，英文是一项必备技能，但是单纯就科研软件来讲，显然使用母语的软件可以减少学习时间成本和使用时间成本，从而加快工作效率。因此，本文的目的是**教会大家如何将 Origin 设置成中文界面**。

在进行下面的操作前**请先关闭 Origin 软件**。

1、打开注册表
-------

同时按 windows 键和 R 键，出现如下界面：

![](https://pic4.zhimg.com/v2-e7e0433fca094730cff8ebb9d6eeec3f_r.jpg)

在方框中输入 regedit， 然后点击确定即可打开注册表。

2、在 Origin 中添加中文值
-----------------

注册表左边的导航栏找到：计算机—>HKEY_CURRENT_USER—>Software—>OriginLab—>Origin 9.7b，如下图。**需要注意的是：**最后一步中的 “Origin 9.7b” 根据个人安装的版本不同会有所不同，我安装的版本是 Origin 2020b，比如如果安装的版本是 Origin 2019b 则最后一步可能为是“Origin 9.6b”。

![](https://pic1.zhimg.com/v2-2263311527ac3c33afc52070cbd59250_r.jpg)

进入 “Origin 9.7b” 后，右键点击右边空白处：新建 —> 字符串值，如下图：

![](https://pic3.zhimg.com/v2-0600373e8e98949876eca707ba31bd0a_r.jpg)

右键点击新建的值，选择重命名，命名为 “Language”。然后右键点击 “Language”，选择修改。如下图：

![](https://pic3.zhimg.com/v2-2b1c8832d1a3f7ed4ce9811f3629d1a6_r.jpg)

选择修改后会出现如下界面：

![](https://pic4.zhimg.com/v2-c3ebdff9889c03f241f53b4c799a0bcb_r.jpg)

在数值数据那一栏中输入 “Chinese”，点击确定，然后关闭注册表。再度打开 Origin，这时可以看到 Origin 就是如下图所示的中文界面了。

![](https://pic2.zhimg.com/v2-31a48131837a6e9bd835b2b668fe5d8d_r.jpg)
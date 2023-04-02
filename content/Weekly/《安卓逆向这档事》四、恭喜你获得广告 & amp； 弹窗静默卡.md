> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.52pojie.cn](https://www.52pojie.cn/thread-1706691-1-1.html)

> [md]# 一、课程目标 ---1. 了解安卓四大组件、Activity 生命周期 2. 弹窗定位、去更新 3. 广告分析与布局优化# 二、工具 ---1. 教程 Demo(更新)2.MT 管理器 / N ... 《安卓逆向这档......

一、课程目标

* * *

1. 了解安卓四大组件、Activity 生命周期  
2. 弹窗定位、去更新  
3. 广告分析与布局优化

二、工具
====

* * *

1. 教程 Demo(更新)  
2.MT 管理器 / NP 管理器  
3. 算法助手  
4. 雷电模拟器  
5. 开发助手

三、课程内容
======

* * *

1. 广告类型
-------

启动广告     弹窗 & 更新广告   横幅广告  

![](https://attach.52pojie.cn/forum/202212/29/105507pyafo8igvkzfqrv0.png)

2. 安卓四大组件
---------

<table><thead><tr><th>组件</th><th>描述</th></tr></thead><tbody><tr><td>Activity(活动)</td><td>在应用中的一个 Activity 可以用来表示一个界面，意思可以理解为 “活动”，即一个活动开始，代表 Activity 组件启动，活动结束，代表一个 Activity 的生命周期结束。一个 Android 应用必须通过 Activity 来运行和启动，Activity 的生命周期交给系统统一管理。</td></tr><tr><td>Service(服务)</td><td>Service 它可以在后台执行长时间运行操作而没有用户界面的应用组件，不依赖任何用户界面，例如后台播放音乐，后台下载文件等。</td></tr><tr><td>Broadcast Receiver(广播接收器)</td><td>一个用于接收广播信息，并做出对应处理的组件。比如我们常见的系统广播：通知时区改变、电量低、用户改变了语言选项等。</td></tr><tr><td>Content Provider(内容提供者)</td><td>作为应用程序之间唯一的共享数据的途径，Content Provider 主要的功能就是存储并检索数据以及向其他应用程序提供访问数据的接口。Android 内置的许多数据都是使用 Content Provider 形式，供开发者调用的（如视频，音频，图片，通讯录等）</td></tr></tbody></table>

### 1.activity 的切换

```
<!---声明实现应用部分可视化界面的 Activity，必须使用 AndroidManifest 中的 <activity> 元素表示所有 Activity。系统不会识别和运行任何未进行声明的Activity。----->
        <activity  
            android:label="@string/app_name"  
            android:  
            android:exported="true">  <!--当前Activity是否可以被另一个Application的组件启动：true允许被启动；false不允许被启动-->
            <!---指明这个activity可以以什么样的意图(intent)启动--->
            <intent-filter>  
                <!--表示activity作为一个什么动作启动，android.intent.action.MAIN表示作为主activity启动--->
                <action  
                    android: />  
                <!--这是action元素的额外类别信息，android.intent.category.LAUNCHER表示这个activity为当前应用程序优先级最高的Activity-->
                <category  
                    android: />  
            </intent-filter>  
        </activity>  
        <activity  
            android: />
        <activity  
            android:  
            android:exported="true" />  
        <activity  
            android:  
            android:exported="true" />  
        <activity  
            android:  
            android:exported="false" />  
        <activity  
            android:  
            android:exported="false" />  
        <activity  
            android: />
```

启动广告流程：  
启动 Activity-> 广告 Activity-> 主页 Activity

修改方法：  
1. 修改加载时间  
2.Acitivity 切换定位，修改 Intent 的 Activity 类名

```
switch (position) {  
            case 0:  
                Intent intent = new Intent();  
                intent.setClass(it.getContext(), ChallengeFirst.class);  
                it.getContext().startActivity(intent);  
                return;  
            case 1:  
                Intent intent2 = new Intent();  
                intent2.setClass(it.getContext(), ChallengeSecond.class);  
                it.getContext().startActivity(intent2);  
                return;  
            case 2:  
                Intent intent3 = new Intent();  //new一个Intent，
                intent3.setClass(it.getContext(), AdActivity.class);  //传入要切换的Acitivity的类名
                it.getContext().startActivity(intent3);  //启动对应的Activity
                return;  
            case 3:  
                Intent intent4 = new Intent();  
                intent4.setClass(it.getContext(), ChallengeFourth.class);  
                it.getContext().startActivity(intent4);  
                return; 
            default:  
                return;  
        }
```

3.Activity 生命周期
---------------

<table><thead><tr><th>函数名称</th><th>描述</th></tr></thead><tbody><tr><td>onCreate()</td><td>一个 Activity 启动后第一个被调用的函数，常用来在此方法中进行 Activity 的一些初始化操作。例如创建 View，绑定数据，注册监听，加载参数等。</td></tr><tr><td>onStart()</td><td>当 Activity 显示在屏幕上时，此方法被调用但此时还无法进行与用户的交互操作。</td></tr><tr><td>onResume()</td><td>这个方法在 onStart() 之后调用，也就是在 Activity 准备好与用户进行交互的时候调用，此时的 Activity 一定位于 Activity 栈顶，处于运行状态。</td></tr><tr><td>onPause()</td><td>这个方法是在系统准备去启动或者恢复另外一个 Activity 的时候调用，通常在这个方法中执行一些释放资源的方法，以及保存一些关键数据。</td></tr><tr><td>onStop()</td><td>这个方法是在 Activity 完全不可见的时候调用的。</td></tr><tr><td>onDestroy()</td><td>这个方法在 Activity 销毁之前调用，之后 Activity 的状态为销毁状态。</td></tr><tr><td>onRestart()</td><td>当 Activity 从停止 stop 状态恢进入 start 状态时调用状态。</td></tr></tbody></table>

![](https://attach.52pojie.cn/forum/202212/29/105514fnc44338qubb43t3.png)

4. 弹窗定位 & 堆栈分析
--------------

修改方法：  
1. 修改 xml 中的 versiocode  
2.Hook 弹窗 (推荐算法助手开启弹窗定位)  
3. 修改 dex 弹窗代码  
4. 抓包修改响应体 (也可以路由器拦截)

5. 布局优化
-------

1. 开发者助手抓布局  
2.MT 管理器 xml 搜索定位  
3. 修改 xml 代码

```
android:visibility="gone"
```

四、课后小作业
=======

* * *

定位并去除作业 demo 首页中的弹窗  
[https://wwl.lanzoub.com/iVKJk0f0pi7g](https://wwl.lanzoub.com/iVKJk0f0pi7g)

[作业反馈贴](https://www.52pojie.cn/thread-1706783-1-1.html)

五、答疑
====

* * *

待更新

六、视频及课件地址
=========

* * *

[百度云](https://pan.baidu.com/s/1cFWTLn14jeWfpXxlx3syYw?pwd=nqu9)  
[阿里云](https://www.aliyundrive.com/s/TJoKMK6du6x)  
[哔哩哔哩](https://www.bilibili.com/video/BV14v4y1D7yA/?vd_source=6dde16dc6479f00694baaf73a2225452)  
PS: 解压密码都是 52pj，阿里云由于不能分享压缩包，所以下载 exe 文件，双击自解压

七、其他章节
======

* * *

[《安卓逆向这档事》一、模拟器环境搭建](https://www.52pojie.cn/thread-1695141-1-1.html)  
[《安卓逆向这档事》二、初识 APK 文件结构、双开、汉化、基础修改](https://www.52pojie.cn/thread-1695796-1-1.html)  
[《安卓逆向这档事》三、初识 smail，vip 终结者](https://www.52pojie.cn/thread-1701353-1-1.html)
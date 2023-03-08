> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [github.com](https://github.com/rpgrpg/freenom-qinglong)

> Automatically Renew Freenom Domain. Contribute to rpgrpg/freenom-qinglong development by creating an ......

[](#freenom-qinglong-域名自动续期-青龙面板)freenom-qinglong 域名自动续期 - 青龙面板
===============================================================

Automatically Renew Freenom Domain for qinglong panle.

[](#已支持多号建议删除旧的定时任务重新拉取)已支持多号，建议删除旧的定时任务，重新拉取。
==============================================

本人没有多号，无法测试。有 bug 请及时反馈，谢谢！

[](#how-to-use食用方法)How to use 食用方法：
===================================

本程序适用于青龙面板 [https://github.com/whyour/qinglong.git](https://github.com/whyour/qinglong.git) ；也支持独立运行，但没有通知推送。

[](#新版青龙)新版青龙：
==============

订阅管理 - 新建订阅 - 名称：自定义，选择单个文件, 链接：[https://raw.githubusercontent.com/rpgrpg/freenom-qinglong/main/freenom.py](https://raw.githubusercontent.com/rpgrpg/freenom-qinglong/main/freenom.py) ，定时规则：自定义，确定之后，点击运行按钮运行一次即可。

[](#旧版青龙)旧版青龙：
==============

无订阅管理，定时任务 - 新建任务 - 名称：自定义，命令：ql raw [https://raw.githubusercontent.com/rpgrpg/freenom-qinglong/main/freenom.py](https://raw.githubusercontent.com/rpgrpg/freenom-qinglong/main/freenom.py) ，定时规则：自定义，确定之后，点击运行按钮运行一次即可。

[](#修改配置文件configsh添加环境变量)修改配置文件 config.sh，添加环境变量
================================================

点击面板左侧的 “配置文件”，然后将文件拉到最后，添加如下两行：export freenom_usr=""，"" 内为你自己的 FREENOM 的用户名，export freenom_psd=""，"" 内为你自己的 FREENOM 密码，多号用 & 分隔

[](#示例)示例：
==========

[](#export-freenom_usr123qqcomabc163comonegmailcom)export freenom_usr="[123@qq.com](mailto:123@qq.com)&[abc@163.com](mailto:abc@163.com)&[one@gmail.com](mailto:one@gmail.com)"
===============================================================================================================================================================================

[](#export-freenom_psd76543210abcdefga1b2c3d4)export freenom_psd="76543210&abcdefg&a1b2c3d4"
============================================================================================

[](#密码带的改密码或添加变量export-change_split把分隔符放里)密码带 “&” 的，改密码或添加变量 export change_split="", 把分隔符放"" 里
==============================================================================================

支持在 freenom.py 文件中直接添加 username 和 password，适用 crontab 等其它定时任务。

[](#freenom是目前全网唯一的免费顶级域名注册网站了大家轻撸避免滥用)freenom 是目前全网唯一的免费顶级域名注册网站了，大家轻撸，避免滥用。
=============================================================================
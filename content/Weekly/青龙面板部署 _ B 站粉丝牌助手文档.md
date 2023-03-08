> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [xiaomiku01.github.io](https://xiaomiku01.github.io/fansMedalHelperVersion/guide/qinglong.html)

> B 站粉丝牌助手文档

*   进入面板，左侧「依赖管理」，点击「新建依赖」，选择 **python、自动拆分**，在名称处粘贴以下内容，点击确定并等待安装完成。
    
    ```
    aiohttp 
    aiohttp_socks
    loguru 
    pyyaml 
    apscheduler
    ```
    
*   左侧「脚本管理」，点击右上角加号，选择 “新建文件”，填写脚本名称 `pull_fansMedalHelper.sh`。
    
    ![](https://xiaomiku01.github.io/fansMedalHelperVersion/assets/image1.e5beb31c.png)
    
*   输入以下内容，点击 “保存”。
    
    ```
    git clone https://github.com/XiaoMiku01/fansMedalHelper.git
    cp fansMedalHelper/users.example.yaml fansMedalHelper/users.yaml
    ```
    
    ![](https://xiaomiku01.github.io/fansMedalHelperVersion/assets/image2.c305351c.png)
    
*   左侧「定时任务」，然后新建任务，名称随便填，命令填 `task pull_fansMedalHelper.sh`, 定时规则随便填，因为这个任务只要执行一次，确定。
    
    ![](https://xiaomiku01.github.io/fansMedalHelperVersion/assets/image3.994e084c.png)
    
*   点击右侧运行，打开日志，等待仓库拉取完成，之后**禁用或者删除这个脚本**。
    
*   回到脚本管理，找到 `fansMedalHelper/users.yaml` 文件，填写自己的配置，点击 “保存”。
    
    ![](https://xiaomiku01.github.io/fansMedalHelperVersion/assets/image5.80b03f9b.png)
    
*   保存后新建定时任务，名称随便填，命令填 `task fansMedalHelper/index.py`, 定时规则填每天执行的时间，确定。
    
    ![](https://xiaomiku01.github.io/fansMedalHelperVersion/assets/image6.d022c2ec.png)
    
*   部署完毕，点击运行测试，查看日志是否正常。
    
    提示
    
    日志中可能出现乱码，是正常现象，因为是输出的日志无法显示文字颜色。
    
*   如何更新 新建一个名为 `update_fansMedalHelper.sh` 的脚本，内容为：
    
    ```
    cd fansMedalHelper
    git pull
    ```
    
    之后创建任务执行这个脚本，命令填 `task update_fansMedalHelper.sh`。运行完成后就更新成功。
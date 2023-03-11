> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.hicairo.com](https://www.hicairo.com/post/55.html)

> 免费节点, 免费 vps,Doprax.com,v2ray,v2ray,nginx+websocket+vmess/vless+tls

**一、Doprax.com 介绍**

Doprax 是丹麦一家企业创建的云平台，功能和 Heroku 及 [Replit](https://www.hicairo.com/post/53.html) 类似。主要基于浏览器的云端协同开发平台，可用于构建开发环境、实时协作、托管网络应用等。Doprax 与 Replit 的主要区别为，Replit 采用 Nix 技术，而 Doprax 采用的是 Docker 技术。当然，使用 Doprax.com 也可以完美搭建 v2ray 节点。

Doprax 官方文档：[https://www.doprax.com/docs/](https://www.doprax.com/docs/)

**二、注册 Doprax.com 账号**

官方地址：[https://www.doprax.com/signup/](https://www.doprax.com/signup/)

注册很简单，只需一个邮箱，接收一下验证码即可完成注册，也可以直接使用 google 账号授权登录。

**三、GitHUB 项目地址**

[https://github.com/hiifeng/V2ray-for-Doprax](https://github.com/hiifeng/V2ray-for-Doprax)

**四、v2ray 节点搭建**

1、登录自己的 GitHUB 账号，打开上述 GitHUB 项目地址，ForK 该项目。

![](https://www.hicairo.com/zb_users/upload/2022/12/20221222192455167170829534633.webp)

2、 登录上一次注册好的 Doprax.com 账号，创建一个新的 APP。

![](https://www.hicairo.com/zb_users/upload/2022/12/20221222192744167170846430657.webp)

3、点击 App name。

![](https://www.hicairo.com/zb_users/upload/2022/12/20221223090216167175733659552.webp)

4、选择从 GitHUB 导入项目，当然如果你实在没有 GitHUB 账号，也可以在  GitHUB 将 6 个文件全部下载到本地，然后通过 Edit source code 将文件上传。

![](https://www.hicairo.com/zb_users/upload/2022/12/20221223090413167175745372744.webp)

5、点击 Connect to GitHub 后，根据提示输入你的 GitHUB 账号及密码，进行授权。

![](https://www.hicairo.com/zb_users/upload/2022/12/20221225203907167197194742979.webp)

6、授权成功后，再次点击左侧菜单中的 Dashboard ，然后点击右侧的 APP name ，然后点击 Import from my GitHub account 按钮后，选择 Import 进行导入。

![](https://www.hicairo.com/zb_users/upload/2022/12/20221225203924167197196473472.webp)

7、导入完成后，点击左侧菜单中的 Deploy 按钮，然后点击右侧的蓝色运行按钮。

![](https://www.hicairo.com/zb_users/upload/2022/12/20221225203939167197197955640.webp)

8、这样节点就启动起来了，灰色的 SSL 盾牌变成了绿色，同时你也可以在底部的黑色窗口中看到 Docker 的启动日志。（注意: 请记住 Doprax 分配的域名，下一步会用到。）

![](https://www.hicairo.com/zb_users/upload/2022/12/202212291672276204365159.webp)

**五、节点服务器端配置**

1、请使用 [第三方工具](https://www.v2fly.org/awesome/tools.html) 生成一个新的 UUID。

2、依次点击左侧菜单中的 Main, 窗口右侧的  Edit source code ，选择 Dockerfile 文件，编辑 UUID 及伪装地址信息，然后保存。

![](https://www.hicairo.com/zb_users/upload/2022/12/202212291672276227538571.webp)

```
# 用新生成的 UUID 替换 de04add9-5c68-8bab-950c-08cd5320df18
ENV UUID de04add9-5c68-8bab-950c-08cd5320df18
# VMESS_WSPATH / VLESS_WSPATH 两个常量分别定义了Vmess/VLess的伪装路径，
# 请分别修改内容中的vmess或vless。注意：伪装路径以 / 符号开始,为避免不必要的麻烦，请不要使用特殊符号.
ENV VMESS_WSPATH /vmess
ENV VLESS_WSPATH /vless
```

3、再次点击左侧菜单中的 Deploy，然后重新启动 APP。

**六、节点客户端配置**

我对 Docker 也不是很熟悉，从接触 Doprax.com 开始，查询 Docker 相关资料，到节点搭建调试成功，用了大概两个小时时间。原本想着将节点链接显示到 Docker 容器的启动日志里，一方面没有找到 Doprax.com 分配的域名变量的获取方法，另外即使想将定义的常量 UUID 显示到启动日志也没有成功，如果你知道这方面信息，请通过 Telegram （[https://t.me/HiaiFeng](https://t.me/HiaiFeng)）告诉我，谢谢

基于此，节点客户端配置需要手动进行，以下我将以 V2rayN 为例。经过上面的步骤，你现在应该知道域名、UUID、VMess 的伪装路径和 VLess 的伪装路径。

1、下图为 VMess 配置示意图，请修改标示内容，其他设置于图片中显示一致。

![](https://www.hicairo.com/zb_users/upload/2022/12/202212291672276258394161.webp)

2、下图为 VLess 配置示意图，请修改标示内容，其他设置于图片中显示一致。

![](https://www.hicairo.com/zb_users/upload/2022/12/202212291672276274474231.webp)

**七、Doprax.com 与  Replit.com 之比较**

1、通过测试，Doprax.com 分配的 IP 地址在德国，速度和   Replit.com 比起来较慢，浏览网页没有问题，但是如果看 youtube ，速度比较拉跨。

2、不过据官方宣称， Doprax.com 是不限流量的，同时永不停机，不会出现   Replit.com 没有流量时，服务自动关闭的问题。另外 Doprax.com 一次只能运行 1 个应用程序。

**八、使用 Cloudflare CDN 对 Doprax.com 节点进行提速**

由于 Doprax.com 速度比较拉跨，如果想高速使用，进行 CDN 加速是很有必要的。这里需要 Cloudflare CDN 反代，而不是简单的打开小黄云，具体教程请参考以下文档：

[https://www.hicairo.com/post/59.html](https://www.hicairo.com/post/59.html)

本文出处：HiFeng'Blog  
本文链接：[https://www.hicairo.com/post/55.html](https://www.hicairo.com/post/55.html)  
版权声明：本博客所有文章除特别声明外，均采用 [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh) 许可协议。转载请注明出处！
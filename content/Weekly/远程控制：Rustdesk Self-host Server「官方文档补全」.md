> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [sspai.com](https://sspai.com/post/80209)

> 本文速通：使用 Rustdesk 自建服务，实现多平台远程操控。

**本文速通**：使用 Rustdesk 自建服务，实现多平台远程操控。自建服务器提升速度和画质。

远程操控
----

远程控制日常是一个常见的需求，但是最近帮女朋友安装软件的时候，发生了一些麻烦的小问题。场景是这样的，她使用的手机是 Android 系统，而她并不会使用 root 提权。所以为了获得控制权限有一定的麻烦。

一个看起来比较可用的方案是「向日葵远程控制」（Sunlogin），但是缺点也非常明显，不能很好适配 Android 客户端。而且在一波操作之后，装了很多软件，控制稳定性也不好，经常断线。为此，我寻找了一下开源的、可自建服务器的软件。很快就发现了「Rustdesk」，事实上，我自己几年前也用过，那个时候的用户数量非常少，直接使用官方服务器甚至都能获得非常流畅的体验。随着近年来的出圈，他们的官方服务器不堪重负，我也随之抛弃了他们。但是这一次为了获得跨平台的远程控制方案，我硬着头皮做了一次部署。

部署的过程踩了很多雷，因为官方文档实在是粗糙了，很多问题并没有说明清楚。在这里提供一份「官方文档补全」供大家参考。

下载安装
----

首先需要找一个可以承载 Rustdesk Server 的服务器，一般的云服务器厂商都可以胜任。我这边使用的是 Ucloud 的廉价服务器。  
 

![](https://cdn.sspai.com/editor/u_chivier/16861284123319.jpg)

[Rustdesk self-host Tutorial](https://sspai.com/link?target=https%3A%2F%2Frustdesk.com%2Fdocs%2Fen%2Fself-host%2F)，官方教程提供了一个可以参考的安装路线，但是其中的很多步骤说明的并不详细。

安装我使用的是最简的下载解压方案，直接下载了 [Github: Rustdesk Server](https://sspai.com/link?target=https%3A%2F%2Fgithub.com%2Frustdesk%2Frustdesk-server) 中的最新版本。

```
wget https://github.com/rustdesk/rustdesk-server/releases/download/1.1.7-4/rustdesk-server-linux-amd64.zip
unzip rustdesk-server-linux-amd64.zip
cd amd64
```

之后看到对应目录下有三个文件：`hbbr`，`hbbs`，`rustdesk-utils`。其中前两个是我们之后需要使用的。

（可选）如果服务器上启用了 ufw，需要对照下面的教程开启部分端口：

```
ufw allow 21115:21119/tcp
ufw allow 8000/tcp
ufw allow 21116/udp
sudo ufw enable
```

参考：[UFW firewall configure for Rustdesk Server](https://sspai.com/link?target=https%3A%2F%2Frustdesk.com%2Fdocs%2Fen%2Fself-host%2Finstall%2F%23if-you-have-ufw-installed-use-the-following-commands-to-configure-the-firewall)

部署服务
----

之后首先进行我们的第一个测试：

```
./hbbr
```

测试 Relay 服务器是否能正常启用。

![](https://cdn.sspai.com/editor/u_chivier/16861284123328.jpg)

但是有一种情况下，可能发生端口重复使用的情况。和老版本的 Rustdesk Server 的一些 bug 有关，会发生类似下面的报错：

![](https://cdn.sspai.com/editor/u_chivier/16861284123334.jpg)

这个时候只能手动 kill 之前已经启用的服务：

![](https://cdn.sspai.com/editor/u_chivier/16861284123338.jpg)

```
sudo netstat -pan | grep ":21117" # 确认端口复用是 hbbr 造成
ps aux | grep hbbr # 确认 hbbr PID
kill xxx(上图中对应的 PID 是 136545)
```

同理，hbbs 服务会占用 21116 端口，检修方案同上。hbbs 服务可以指定一个 Relay 服务器，所以我和官方文档中启用顺序不同，先启用 hbbr，之后启用 hbbs。（但是理论上应该没有影响，我这样操作个人觉得更符合逻辑）

pm2 自动启动
--------

为了方便自动启动，文档中提到了使用 pm2 进行管理。我这里也参考官方文档进行一些补充。

首先是 npm 的安装，这里可以直接偷懒使用 apt 安装：

```
sudo apt install npm
sudo npm install -g pm2
```

之后使用 npm 启动「当前目录下下载好的 hbbr 和 hbbs」

```
pm2 start ./hbbr
pm2 start ./hbbs -- -r [Server IP]
```

然后可以在 `pm2 list` 命令的帮助下查看运行状况：  
 

![](https://cdn.sspai.com/editor/u_chivier/16861284123342.jpg)

如果这里出现了 error 或者 stopped，有两个主要的可能性：

1.  之前的端口冲突了，使用上文的方法检查端口使用情况
2.  使用云服务器厂商需要检查一下防火墙设置是否打开了 21115-21119 的 TCP，其中 21116 同时需要 TCP 和 UDP。这里是在云服务器管理页面进行设置。（为了偷懒，我直接把自己的服务器 2000-60000 的端口全部打开了，大家不要学习）

![](https://cdn.sspai.com/editor/u_chivier/16861284123346.jpg)

pm2 的状态正常之后，可以使用 `pm2 save` 存储 pm2 正在管理的任务。

客户端配置
-----

在 Rustdesk 官网下载最新的客户端之后，点击红框进入设置页面。

![](https://cdn.sspai.com/editor/u_chivier/16861284123350.jpg)

之后进入 network 进行相应的配置：

![](https://cdn.sspai.com/editor/u_chivier/16861284123354.jpg)

这里 Unlock 之后只需要填写 ID Server 和 Relay Server 即可。填写的时候需要说明连接端口。例如此处我在 ID Server 填写的是 `xxx.xxx.xxx.xxx:21116`，Relay Server 填写的是 `xxx.xxx.xxx.xxx:21117`。

填写完之后，回到 Rustdesk 连接页面上，可以看到下放再一次变成 Ready 状态了；

![](https://cdn.sspai.com/editor/u_chivier/16861284123357.jpg)

之后和任何配置好服务器的设备都可以互相进行远程控制。
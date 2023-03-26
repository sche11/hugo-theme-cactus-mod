> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.jinjun.top](https://www.jinjun.top/444.html)

> Zerotier 这个软件稳定使用半年以上了，但是存在一点小问题，晚上延迟会高点。在网上也搜索到不少的解决方案，搭建 moom 服务来中续，效果好一点。偶然在搜索的时候，发现可以自建一个 planet...

Zerotier 这个软件稳定使用半年以上了，但是存在一点小问题，晚上延迟会高点。在网上也搜索到不少的解决方案，搭建 moom 服务来中续，效果好一点。偶然在搜索的时候，发现可以自建一个 planet 核心节点，就尝试一下安装。  

### 服务概念

*   Planet：就类似官方的行星服务器，用来管理 zerotier 客户端的地址信息，帮助建立客户端之间的链接，以及无法建立直接的链接的时候，可以作为中续服务器来转发客户端之间的流量。
*   moom：作为中续服务器存在，官方节点的都在海外，建立国内节点做为中续，可以使转发的效率更高，延迟也低。

### 服务器选择

这里我选择了一个吃灰的服务器，腾讯的 4H4G8M 活动机。国内主流的云服务提供商：腾讯云、华为云、阿里云等等，当然配置不要太高，转发速度主要看带宽，单核、128m、5G 硬盘、1M 带宽，我测试可以运行，满足这个基本配置以上都可以跑起来了。这里我选择 Debian 11.1 的系统。

### 安装 Planet

#### 升级系统软件包

__复制

```
apt-get upgrade
apt-get dist-upgrade
```

#### 安装 Zerotier 和 Ztncui

作者文档：[一键搭建 zerotier planet 服务器脚本_独步 - 的博客](https://blog.csdn.net/opopop880/article/details/122880479 "垃圾中文技术性网站")  
一键脚本仓库地址：[opopop880/zerotier_planet](https://gitee.com/opopop880/zerotier_planet)

*   适合于 Debian 和 Ubuntu 安装

需要 root 权限执行

__复制

```
wget https://gitee.com/opopop880/zerotier_planet/raw/master/zerotier_planet_debain.sh && chmod +x zerotier_planet_debain.sh && ./zerotier_planet_debain.sh
```

*   适用 redhat centos 安装

__复制

```
wget https://gitee.com/opopop880/zerotier_planet/raw/master/zertotier_planet.sh && chmod +x zertotier_planet.sh && ./zertotier_planet.sh
```

Debian 和 Ubuntu、如果 zerotier 编译过程中提示`nlohmann/json.hpp`找不到的问题，需要安装 nlohmann-json-dev 软件包

__复制

```
wget http://kr.archive.ubuntu.com/ubuntu/pool/universe/n/nlohmann-json/nlohmann-json-dev_2.1.1-1.1_all.deb && dpkg -i nlohmann-json-dev_2.1.1-1.1_all.deb
```

##### 查看监听端口

![](https://img.jinjun.top/images/2023/01/26/bc75b3c79e3fadc75b2e0a03af8e35ff.png)

出现 zerotier-one 和 ztncui 相对应的进程和端口

##### 查看管理页面

执行完成后，打开 ip:3000 或者 [https://ip:3443](https://ip:3443/)，用户名`admin` 密码`password`

![](https://img.jinjun.top/images/2023/01/26/174bcb62197231942c4fa03adfece762.png)

能打开页面表示服务器安装成功，安装完成会在执行目录，生成`planet`文件，找到这个文件并下载下来。

### 云服务器放行规则

*   TCP：3000、3443、9993
*   UDP：9993
*   3000 端口是控制台的 http
*   3443 端口是控制台的 https
*   9993 端口是 planet 的根服务器之间通讯

### 创建网络

![](https://img.jinjun.top/images/2023/01/26/022327d718b83f223b49c4ac03ba18e5.png)

### 配置网络

控制台找到 - 网络 - 简易安装 - 生成网络地址 - 提交保存

![](https://img.jinjun.top/images/2023/01/26/73f891ba5300b929f7330d63ada05ce8.png)

### 配置 ipv4 和 ipv6 分配模式

![](https://img.jinjun.top/images/2023/01/26/a903258019b8e68ad17486cd5026f2a1.png)

![](https://img.jinjun.top/images/2023/01/26/506e67dfe9a83ba92e4ec2b74244c8cf.png)

### 配置 zerotier 客户端

#### Linux 端

官方安装方式

__复制

```
netstat -tunlp
```

在`/var/lib/zerotier-one/` 找到刚刚下载的 planet，上传替换

![](https://img.jinjun.top/images/2023/01/26/340859f85c53525f087aed2465545984.png)

重启 zerotier

__复制

```
curl -s https://install.zerotier.com | sudo bash
```

加入网络，在控制台找到 `网络ID` 复制下来

__复制

```
systemctl restart zerotier-one.service
```

加入网络后，需要在控制台点授权和分配 IP 才能正常使用

![](https://img.jinjun.top/images/2023/01/26/ab8c8bc3844314c003e4647607a74433.png)

运行`zerotier-cli listpeers` 检查是否加入根服务器

![](https://img.jinjun.top/images/2023/01/26/66d32b700699766b3f2480bd4e26b412.png)

这里的 IP 都是自己的设备，已经完成组网的设备，如果出现海外 IP，可能是文件替换了没有重启、要排除海外 IP 组网。

#### Winows 端

下载地址：[Download -- ZeroTier](https://www.zerotier.com/download/)

点自动安装后，默认会在任务栏启动，需要在右下角找到 zerotierUI 点击 Quit 退出

*   停止 Zerotier 任务

![](https://img.jinjun.top/images/2023/01/26/c5081eba803b112e00300c2aea68c6aa.png)

*   替换 planet 文件

打开`C:\ProgramData\ZeroTier\One`，用刚刚下载的 planet 替换掉本地的 planet

![](https://img.jinjun.top/images/2023/01/26/b147bd186f818eca6c003aa2dc32d18e.png)

*   重启 Zerotier 服务

在任务管理器点击重新启动 Zerotier 服务，等已停止变成正在运行

*   连接私有网络

在控制台找到你想加入网络的 `网络ID`，复制下来

![](https://img.jinjun.top/images/2023/01/26/83a264a8359272be4bb685545820cf47.png)

打开 ZerotierUI，在任务栏找到 右键 - join New Network

![](https://img.jinjun.top/images/2023/01/26/61a3b3d23f421d1b6428a3ce3659dfc3.png)

在服务端界面，给本地客户端授权

![](https://img.jinjun.top/images/2023/01/26/2c55cb5c2e64f1cae8d2e2c2f1519f70.png)

在客户端查看状态 OK 表示连接成功。

#### 安卓端

安卓端的开源地址：[https://github.com/kaaass/ZerotierFix](https://github.com/kaaass/ZerotierFix)

找到刚才下载的 planet 的文件，然后通过软件加载下载的 planet 文件即可。

然后添加网络 ID，然后去控制台授权当前设备就可以愉快玩耍了。

![](https://img.jinjun.top/images/2023/01/26/370e1a2650b3f8387ac2209ca9b8840e.jpg)

#### Linux 图形化桌面端

Linux 端的开源地址：[https://github.com/tralph3/ZeroTier-GUI](https://github.com/tralph3/ZeroTier-GUI)

下载源码后进行解压，然后执行编译安装

### 测试网络

#### 延迟测试

*   使用 ping 测试
*   客户端距离 (客户端位于深圳到广西)，延迟还是很低的

![](https://img.jinjun.top/images/2023/01/26/6d9f861807fad84a057473217502d469.png)
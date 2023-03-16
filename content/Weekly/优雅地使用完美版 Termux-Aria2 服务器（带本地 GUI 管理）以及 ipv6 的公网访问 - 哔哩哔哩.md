> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.bilibili.com](https://www.bilibili.com/read/cv14084579)

> 前言：我认为你会看这篇文章之前必是初步了解过 Aria2 的，但为防初学者只是找一个下载工具便凑巧点了进来，我也引用 Aria2 中文网的简介大致说明一下。

前言：我认为你会看这篇文章之前必是初步了解过 Aria2 的，但为防初学者只是找一个下载工具便凑巧点了进来，我也引用 Aria2 中文网的简介大致说明一下。

> 免费轻量级命令行下载工具: Aria2
> 
> Aria2 是一款开源下载工具，可帮助简化不同设备和服务器之间的下载过程。它支持磁力链接、BT 种子、http 等类型的文件下载，与迅雷及 QQ 旋风相比，Aria2 有着优秀的性能及较低的资源占用, 架构本身非常轻巧，通常只需要 4 兆字节（HTTP 下载）到 9 兆字节（用于 BitTorrent 交互）之间。最重要的一点是 Aria2 完全免费！
> 
> ———引用自 http://aria2.baisheng999.com/

在使用 Aria2 之前，我首先提醒：

1.  Aria2 无法下载迅雷专用链接！
    
2.  不建议使用迅雷私有链接，迅雷软件是有原罪的。它（与封杀 bt 的运营商）从根本上破坏了 BT 的生态。
    

![](http://i0.hdslb.com/bfs/article/4aa545dccf7de8d4a93c2b2b8e3265ac0a26d216.png)

那么进入正题，Termux, 是一个运行在 Android 上的终端模拟器（Terminal），如 konsole 对于 KDE、Terminal.app 对于 Mac，终端模拟器提供了命令行对硬件资源的访问形式，虽然 Termux 的工作环境被 Android 限制，但是，说它是 Android 平台最优秀的终端模拟器是毫无疑问的。

在搜索引擎上随便搜索一番，你会看到很多稀奇古怪的 Termux 使用方式，比如安装一个运行在 proot 下的 linux 环境、运行各种 python 工具等等。这已经是最大限度地对 Termux 进行了开发，让 Termux 成为了一个很有意思的工具。

下载 Termux 以及基本使用请去：

```
https://f-droid.org/zh_Hans                   //Termux下载网站
https://www.sqlsec.com/2018/05/termux.html    //新手入门教程
```

而 Termux 源中原生包含了 Aria2, 只需要使用：

```
pkg install aria2
```

就可以进行安装，而安装之后，aria2 就是可以使用了的，最简单的使用方式就是 cd 到想要存放文件的文件夹，使用 Aria2c [链接] 的方式进行文件下载。

但是，更多时候，Aria2 是需要作为服务一直运行的。它有一个可以通过本地终端的网络浏览器打开的管理页面，而这个页面，不仅仅是本地的终端才能够打开，只要局域网下的终端访问运行 Aria2 服务的终端端口，那么也可以打开这个页面。甚至如果你有公网 ip 的话，可以通过互联网直接访问家中的 Aria2 服务器进行远程管理。

如今 ipv4 的公网 ip 自然是一址难求，但是 ipv6 的地址却是不限量供应，在可以预见的未来十年，ipv6 在家庭和个人的服务上会大行其道。譬如家庭的云储存、云服务，甚至是基于家庭的云计算，这都需要公网 ip 的支持，而 ipv4 注定承载不起这样的重担。

而运行 Aria2 服务，除了程序本身以外，还需要配置文件、日志文件、以及数据（也可称为会话）文件。

其中，日志文件和数据文件只需要创建出来，任由 Aria2 程序操作即可，配置文件相当于 Aria2 的设置，马虎不得。这个文件中需要注意的有下载文件夹的位置、数据文件和日志文件的位置，而这个文件内容的模板，我会在下面贴出。

```
aria2.conf           //配置文件 相当于设置。
aria2.session        //数据文件 存放断点续传、下载文件等数据。
aria2.log            //日志文件 用于查错等，甚至可以不用。
```

创建文件的命令是 touch, 例如：

```
touch aria2.conf
```

一般我会在 Termux 用户目录中的. config 文件夹中创建 aria2 文件夹去存放这几个文件，这取决于个人喜好。只要你能够找得到，可以随便放。

在创建这三个文件后，

```
touch aria2.conf
touch aria2.log
touch aria2.session
```

再编辑 aria2.conf 文件，使用 vim、nano 都可以。

```
vim aria2.conf
```

打开现在还是空白的 aria2.conf 文件，之后将如下内容写入：

```
##===================================##
## 文件保存相关 ##
##===================================##

# 文件保存目录
dir=[下载文件夹位置]
# 启用磁盘缓存, 0为禁用缓存, 需1.16以上版本, 默认:16M
disk-cache=16M
# 断点续传
continue=true
#日志保存
log=[日志文件位置/aria2.log]

# 文件预分配方式, 能有效降低磁盘碎片, 默认:prealloc
# 预分配所需时间: none < falloc ? trunc < prealloc
# falloc和trunc则需要文件系统和内核支持
# NTFS建议使用falloc, EXT3/4建议trunc, MAC 下需要注释此项
file-allocation=prealloc

##===================================##
## 下载连接相关 ##
##===================================##

# 最大同时下载任务数, 运行时可修改, 默认:5
max-concurrent-downloads=10
# 同一服务器连接数, 添加时可指定, 默认:1
# 官方的aria2最高设置为16, 如果需要设置任意数值请重新编译aria2
max-connection-per-server=16

# 整体下载速度限制, 运行时可修改, 默认:0（不限制）
max-overall-download-limit=0
# 单个任务下载速度限制, 默认:0（不限制）
max-download-limit=0
# 整体上传速度限制, 运行时可修改, 默认:0（不限制）
max-overall-upload-limit=0
# 单个任务上传速度限制, 默认:0（不限制）
max-upload-limit=0

# 禁用IPv6, 默认:false
disable-ipv6=false

# 最小文件分片大小, 添加时可指定, 取值范围1M -1024M, 默认:20M
# 假定size=10M, 文件为20MiB 则使用两个来源下载; 文件为15MiB 则使用一个来源下载
min-split-size=10M

# 单个任务最大线程数, 添加时可指定, 默认:5
# 建议同max-connection-per-server设置为相同值
split=16

##===================================##
## 进度保存相关 ##
##===================================##

# 从会话文件中读取下载任务
input-file=[数据文件保存位置/aria2.session]
# 在Aria2退出时保存错误的、未完成的下载任务到会话文件
save-session=[数据文件保存位置/aria2.session]
# 定时保存会话, 0为退出时才保存, 需1.16.1以上版本, 默认:0
save-session-interval=60


##===================================##
## RPC相关设置 ##
##此部分必须启用，否则无法使用WebUI
##===================================##

# 启用RPC, 默认:false
enable-rpc=true
# 允许所有来源, 默认:false
rpc-allow-origin-all=true
# 允许外部访问, 默认:false
rpc-listen-all=true
# RPC端口, 仅当默认端口被占用时修改

rpc-listen-port=6800
# 设置的RPC授权令牌, v1.18.4新增功能, 取代 --rpc-user 和 --rpc-passwd 选项
#rpc-secret=

# 设置的RPC访问用户名, 此选项新版已废弃, 建议改用 --rpc-secret 选项
#rpc-user=
# 设置的RPC访问密码, 此选项新版已废弃, 建议改用 --rpc-secret 选项
#rpc-passwd=

# 启动SSL
# rpc-secure=true
# 证书文件, 如果启用SSL则需要配置证书文件, 例如用https连接aria2
# rpc-certificate=
# rpc-private-key=

##===================================##
## BT/PT下载相关 ##
##===================================##

# 当下载的是一个种子(以.torrent结尾)时, 自动开始BT任务, 默认:true
follow-torrent=true
# BT监听端口, 当端口被屏蔽时使用, 默认:6881-6999
listen-port=51413
# 单个种子最大连接数, 默认:55
#bt-max-peers=55
# 打开DHT功能, PT需要禁用, 默认:true
enable-dht=true
# 打开IPv6 DHT功能, PT需要禁用
enable-dht6=true
# DHT网络监听端口, 默认:6881-6999
dht-listen-port=6881-6999

# 本地节点查找, PT需要禁用, 默认:false
bt-enable-lpd=true
# 种子交换, PT需要禁用, 默认:true
enable-peer-exchange=true
# 每个种子限速, 对少种的PT很有用, 默认:50K
bt-request-peer-speed-limit=50K

# 客户端伪装, PT需要
peer-id-prefix=-TR2770-
user-agent=Transmission/2.77

# 当种子的分享率达到这个数时, 自动停止做种, 0为一直做种, 默认:1.0
seed-ratio=0
# 强制保存会话, 即使任务已经完成, 默认:false
# 较新的版本开启后会在任务完成后依然保留.aria2文件
force-save=true
# BT校验相关, 默认:true
#bt-hash-check-seed=true
# 继续之前的BT任务时, 无需再次校验, 默认:false
bt-seed-unverified=true
# 保存磁力链接元数据为种子文件(.torrent文件), 默认:false
bt-save-metadata=true
# 单个种子最大连接数, 默认:55 0表示不限制
bt-max-peers=0
# 最小做种时间, 单位:分
# seed-time = 60
# 分离做种任务
bt-detach-seed-only=true
#BT Tracker List ;下载地址：https://cdn.jsdelivr.net/gh/XIU2/TrackersListCollection/best_aria2.txt
#页面地址：https://github.com/XIU2/TrackersListCollection/blob/master/README-ZH.md
bt-tracker=http://all4nothin.net:80/announce.php,http://kinorun.com:80/announce.php,http://masters-tb.com:80/announce.php,http://mediaclub.tv:80/announce.php,http://milanesitracker.tekcities.com:80/announce,http://nyaa.tracker.wf:7777/announce,http://open.acgnxtracker.com:80/announce,http://openbittorrent.com:80/announce,http://opentracker.xyz:80/announce,http://share.camoe.cn:8080/announce,http://t.nyaatracker.com:80/announce,http://torrent-team.net:80/announce.php,http://torrentzilla.org:80/announce,http://torrentzilla.org:80/announce.php,http://tr.cili001.com:8070/announce,http://tracker.files.fm:6969/announce,http://tracker.gbitt.info:80/announce,http://tracker.ipv6tracker.ru:80/announce,http://tracker.tfile.me:80/announce,http://tracker.torrentyorg.pl:80/announce,http://vps02.net.orel.ru:80/announce,http://www.all4nothin.net:80/announce.php,https://1337.abcvg.info:443/announce,https://carbon-bonsai-621.appspot.com:443/announce,https://tr.ready4.icu:443/announce,https://tr.torland.ga:443/announce,https://tracker.imgoingto.icu:443/announce,https://tracker.kuroy.me:443/announce,https://tracker.lilithraws.cf:443/announce,https://tracker.nitrix.me:443/announce,https://tracker.parrotsec.org:443/announce,https://tracker.tamersunion.org:443/announce,https://trackme.theom.nz:443/announce,udp://9.rarbg.com:2810/announce,udp://abufinzio.monocul.us:6969/announce,udp://bt1.archive.org:6969/announce,udp://bt2.archive.org:6969/announce,udp://code2chicken.nl:6969/announce,udp://discord.heihachi.pw:6969/announce,udp://engplus.ru:6969/announce,udp://escorts.subventas.com:53/announce,udp://exodus.desync.com:6969/announce,udp://fe.dealclub.de:6969/announce,udp://ipv6.tracker.monitorit4.me:6969/announce,udp://ipv6.tracker.zerobytes.xyz:16661/announce,udp://jeremylee.sh:6969/announce,udp://mail.realliferpg.de:6969/announce,udp://movies.zsw.ca:6969/announce,udp://open.demonii.com:1337/announce,udp://open.tracker.cl:1337/announce,udp://opentor.org:2710/announce,udp://p4p.arenabg.com:1337/announce,udp://retracker.hotplug.ru:2710/announce,udp://thetracker.org:80/announce,udp://tracker-de.ololosh.space:6969/announce,udp://tracker.0x.tf:6969/announce,udp://tracker.altrosky.nl:6969/announce,udp://tracker.auctor.tv:6969/announce,udp://tracker.beeimg.com:6969/announce,udp://tracker.birkenwald.de:6969/announce,udp://tracker.bitsearch.to:1337/announce,udp://tracker.blacksparrowmedia.net:6969/announce,udp://tracker.dler.com:6969/announce,udp://tracker.haynet.io:6969/announce,udp://tracker.jordan.im:6969/announce,udp://tracker.leech.ie:1337/announce,udp://tracker.moeking.me:6969/announce,udp://tracker.monitorit4.me:6969/announce,udp://tracker.ololosh.space:6969/announce,udp://tracker.openbittorrent.com:6969/announce,udp://tracker.opentrackr.org:1337/announce,udp://tracker.pomf.se:80/announce,udp://tracker.theoks.net:6969/announce,udp://tracker.tiny-vps.com:6969/announce,udp://tracker.torrent.eu.org:451/announce,udp://tracker.zerobytes.xyz:1337/announce,udp://tracker0.ufibox.com:6969/announce,udp://tracker1.bt.moack.co.kr:80/announce,udp://tracker2.dler.com:80/announce,udp://tracker2.dler.org:80/announce,udp://u.wwwww.wtf:1/announce,udp://udp-tracker.shittyurl.org:6969/announce,udp://vibe.sleepyinternetfun.xyz:1738/announce,udp://www.torrent.eu.org:451/announce,wss://tracker.openwebtorrent.com:443/announce
```

其中需要修改的是日志文件保存位置和数据文件保存位置。按照自己存放 aria2.log 和 aria2.session 文件的位置写入。另外，有 bt-tracker 的部分为我个人用于下载 bt 的设置。而获取地址在 bt-tracker 地址上方已经备注，可自行更换（与本文关系不大）。

至此，工作完成了最大的主体部分，其余的，都是锦上添花。

```
aria2c --conf-path=[aria2.conf文件路径/aria2.conf]    //启动服务，注意程序是aria2而命令为aria2c
```

服务已经运行起来了，它显示：

```
11/20 12:08:26 [NOTICE] IPv4 RPC: listening on TCP port 6800
11/20 12:08:26 [NOTICE] IPv6 RPC: listening on TCP port 6800
```

这时候，你需要一个 GUI 的软件或者一个管理页面去访问这个存在于 6800 端口的服务，我倾向于使用这个页面

```
http://mirror-aria2.qingxu.live/
```

这是一个存放于互联网的站点，通过访问本地端口的形式进行 Aria2 的管理 / 使用。这是一个很方便也足够优雅的方式，除非这个站点不再能够访问了。

进入管理页面以后，你会看到：

![](http://i0.hdslb.com/bfs/article/watermark/2a4625ea9aeb7b9103ec42f1e49f617ca09aedf6.png@942w_329h_progressive.webp)Aria2 管理 / 设置页面

现在，你就已经可以使用 Aria2 了。

![](http://i0.hdslb.com/bfs/article/02db465212d3c374a43c60fa2625cc1caeaab796.png)

但是，问题来了——它不够优雅。

比如：

1.  每次在进入 Termux 之后都需要手动运行服务。
    
2.  命令行太长
    
3.  每次运行服务之后都会在前台显示甚至在运行时不断输出日志。
    
4.  某些情况下基于互联网的管理界面访问不了。
    

由于这篇文章是要有一个在 Termux 上运行 Aria2 的完美方案，那就不能将就，不能以 “又不是不能用” 作为原则。

基于这些因素，接下来要解决的问题有：

1.  后台运行 Aria2 服务
    
2.  基于第 1 点自动后台运行 Aria2 后台服务
    
3.  运行本地管理服务（本地管理页面）
    
4.  基于第 3 点，自动运行本地管理服务
    
5.  在即便服务挂掉之后也可以使用较短的命令启动服务
    

只需要在运行服务的时候在命令后面加一个  -D 即可：

```
aria2c --conf-path=[配置文件地址/aria2.conf] -D
```

这时候我们需要编辑在 Termux 用户目录下的. bashrc 或者你与我一样使用 OMZ, 便可以编辑. zshrc 文件，在文件中添加命令

```
aria2c --conf-path=[配置文件地址/aria2.conf] -D
```

那么，在每次启动 Termux 时，这个命令会自动后台运行，无需手动操作。

也是要编辑. bashrc 或者. zshrc 文件，在自动后台运行 Aria2 服务的命令前面添加如下行：

```
alias start-aria2c='aria2c --conf-path=[配置文件地址/aria2.conf] -D'
```

之所以要在运行 Aria2 的命令前头添加是因为——我个人习惯。因为这时候就不必使用比较长的自动后台运行命令了。alias 已经定义了 start-aria2c 这个短命令所执行的操作就是 aria2c --conf-path=[配置文件地址 / aria2.conf] -D。那么在 alias 定义以后，便可以不使用这个长命令来执行自动操作了。

完成之后添加的内容便是：

```
alias start-aria2c='aria2c --conf-path=[配置文件地址/aria2.conf] -D'  //定义命令
start-aria2c                                                          //启动Termux后自动运行命令
```

这时候，就需要运行另外一个服务了，它依赖 nodejs, 所以你需要：

```
pkg install nodejs-lts
```

还需要下载运行 nodejs 服务所需要的文件，获取方式为：

```
git clone https://github.com/ziahamza/webui-aria2.git
```

如果没有 git 工具，也请下载：

```
pkg install git
```

在下载完成后，当前目录便存在一个文件夹，你可以和我一样，用 mv 命令把它放在那三个文件同样的位置，即：~/.config/aria2 中。

进入刚刚下载的文件夹：

```
cd ~/.config/arai2/webui-aria2
```

这时候就可以运行 nodejs 了：

```
node node-server.js
```

运行结果是：

```
WebUI Aria2 Server is running on http://localhost:8888
```

可以在浏览器中输入 http://localhost:8888 进行访问，或者可以在同一局域网中输入：[手机 ip]:8888 进行访问。

页面在电脑上显示如下：

![](http://i0.hdslb.com/bfs/article/watermark/d0026d22958d734df7f5e961bcd28e27b596d417.png@942w_290h_progressive.webp)通过局域网访问

一样，它也存在和 Aria2 同样的问题——不够优雅。

而为了让它更加优雅，解决管理界面的后台运行，需要使用到 nohup 这个工具，你依旧可以使用 pkg 进行下载，感谢开发者和社区的贡献者！

```
pkg install nohup
```

nohup 将服务的输出结果放到 nohup.txt 文件中，不再将输出到终端屏幕上。

使用：

```
nohup node [文件路径]node-server.js &
```

运行的管理服务将后台运行，足够优雅。

与 Aria2 类似的方式，将：

```
nohup node [文件路径]node-server.js &
```

用 alias 定义为 start-aria2-ui, 再自动运行

```
vim .zshrc  or vim .bashrc    //编辑文件
//添加：
alias start-aria2-ui='nohup node [文件路径]node-server.js &'
start-aria2-ui   //运行
```

这时候，每次启动 Termux 的时候，Aria2 以及 Aria2 管理服务就会自动运行了，而如果某种原因导致了服务中断，也可以优雅地使用短命令 start-aria2 以及 start-aria2-ui 重启服务。不过也可以不优雅地关掉 Termux 重启，命令也会自动重启。

![](http://i0.hdslb.com/bfs/article/db75225feabec8d8b64ee7d3c7165cd639554cbc.png)

以上，就已经可以优雅地使用完美版的 Aria2 和管理服务了。那么，再上一步呢？如何进行远程管理，也就是说不在局域网下访问服务呢？

那就需要有一个公网地址，如果你在使用长城、方正等宽带那你得到公网 ip 的可能性就很小了，以及你在使用移动宽带，获取公网 ip 恐怕需要很大力地争取。

电信和联通，这两家在全国基本上已经覆盖了 ipv6 地址的下发，甚至在某些时候，在强力要求下能够下发公网 ipv4 的 ip 地址。而除了运营商，你还需要一个能够获取 ipv6 的路由器，而即便你拥有支持 ipv6 的路由器，你还需要光猫改为桥接模式或者直接使用光猫本身的路由服务（然而并非所有的光猫都提供了 ipv6 的获取），因为如果有两层路由，你的设备获取到的是第二层路由下发的局域网 ip, 无法得到 ipv6 地址。

如果你有幸，获取到了公网 ip，那么，你在局域网上所有开放的端口将在互联网上开放，虽然 ipv6 地址浩如烟海，直接得到你的 ipv6 地址也是一件费力气的事情，但在你访问 ipv6 网址时，你的 ipv6 地址表示这个地址将实实在在地存在一段时间，直到运营商下发或者你手动获取另外一个地址。这导致了一部分的安全问题，所以要谨慎。

其中，我们可以对 Aria2 进行令牌的设置，这可以看作是一个没有用户名的密码，而设置方式就是编辑 aria2.conf 文件，取消其中 #rpc-secret = 行的注释，也就是删除 #，接着在 = 后面写入你想要使用的令牌。（ps：Aria2 存在用户名 + 密码的授权方式，但是用户名 + 密码进行授权的方式已经不建议使用了）

在管理界面的设置中，你要填写上这个令牌才能够使用 Aria2 服务。

接下来，由于我的移动网络获取不到 ipv6 的公网地址，我会使用电脑作为服务端，使用手机进行访问。

先 ping 一下，而 ping ipv6 的方式不同于 ipv4, 要使用 ping6

```
ping6 240e:***:95:****:3c64:5363:d883:****    //隐私打码，虽然必要性不是太高
```

```
PING 240e:***:95:****:3c64:5363:d883:****(240e:***:95:****:3c64:5363:d883:****) 56 data bytes
64 bytes from 240e:***:95:****:3c64:5363:d883:****: icmp_seq=1 ttl=51 time=41.1 ms
64 bytes from 240e:***:95:****:3c64:5363:d883:****: icmp_seq=2 ttl=51 time=57.7 ms
64 bytes from 240e:***:95:****:3c64:5363:d883:****: icmp_seq=3 ttl=51 time=43.3 ms
64 bytes from 240e:***:95:****:3c64:5363:d883:****: icmp_seq=4 ttl=51 time=46.3 ms
64 bytes from 240e:***:95:****:3c64:5363:d883:****: icmp_seq=5 ttl=51 time=37.6 ms
64 bytes from 240e:***:95:****:3c64:5363:d883:****: icmp_seq=6 ttl=51 time=44.1 ms
```

ping 通了，说明从公网是可以找到我的 ipv6 地址的。

接下来用手机访问：

```
[240e:***:95:****:3c64:5363:d883:****]:8888    //8888就是管理的开放端口
```

![](http://i0.hdslb.com/bfs/article/watermark/46938b3306a92868e12ada962d07b224a94ceb19.jpg@942w_2010h_progressive.webp)远程访问

注意：在手机端浏览器中输入 ipv6 地址需要用 [方括号] 给括起来，Android-chrome 是这样的，其他平台以及浏览器请自行测试。

在成功访问后，在设置中输入令牌，连接到 Aria2！！

![](http://i0.hdslb.com/bfs/article/4adb9255ada5b97061e610b682b8636764fe50ed.png)

你甚至可以买一个冷门域名，这样通过动态解析，即便是动态的 ipv6 地址，也可以在固定的网页地址访问。这就属于另一个范围了，但在 ipv6 彻底普及之后，显然以家庭或者公司（尤其是小公司）为中心的云方案会如雨后春笋不断出现，ipv6 甚至会成为产业变革的核心。

但是商业公司（尤其是大型公司）不可能会愿意见到个人过多使用自身的资源，而是希望用户去使用他们的服务。比如 BT 的存在（由于 ipv6 是公网，运营商不太可能去封锁，于是 BT 会成为真正流行的资源分享方式，当然也要警惕吸血雷和一些吸血的 BT 播放器）有可能会极大冲击网盘的利益。

还有家庭的服务器，比如家庭电脑上运行的网盘，动辄 1T2T 的电脑硬盘通过公网地址能够访问的情况下，何必用某某网盘呢？

去中心化所必须的公网 ip, 在 ipv6 的时代已经不再昂贵，这些，也许能够彻底推动去中心化这个时代的到来。而去中心化，那就是让每个人都能够成为一个中心。

这篇文章所写的 Aria2, 不止是一个 Aria2。
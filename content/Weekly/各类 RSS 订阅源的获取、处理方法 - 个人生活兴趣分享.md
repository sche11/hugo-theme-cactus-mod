> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.yanzhihome.com](https://www.yanzhihome.com/1177.html)

> 可以用浏览器插件 Shoyu RSS、Atom Feed Preview，插件 Tampermonkey 的 RSS＋、RSSHelper 油猴脚本，在浏览网站时，直接页面右下方显示该网站 RSS 订阅源（前提是该网站提供了 RSS 支持服务）。

一、RSS通用订阅
---------

1. RSS-Proxy  

---------------

RSS-Proxy 可以针对 RSSHub 未支持抓取的网站，提供个人自主生成网站 RSS 链接的服务。

这是公用示例网址 [RSS-proxy playground (migor.org)](https://rssproxy-v1.migor.org/)。

也可以 Docker 部署：

```
docker pull damoeb/rss-proxy
docker run -p 3000:3000 -it damoeb/rss-proxy
```

打开 RSS-Proxy 链接后，在有上角输入要抓取的网站链接，点击 “show Feeds”，然后点击右下角的按钮，

![](https://img.yanzhihome.com/image-20220503175223150.png)

在浏览器地址栏获取生成的订阅链接。

![](https://img.yanzhihome.com/image-20220503175551957.png)

### 2. Huginn

**2.1 Docker-compose** 部署

huginn 可以直接登入官网使用，也可以自行部署，这里提一下 docker-compose 部署。

在宝塔后台文件目录，新建 docker-compose.yml 文件，打开后，将下面的代码贴入保存。

```
version: "3.5"
services: 
    huginn-server:
        image: huginn/huginn
        container_name: huginn
        depends_on: 
            - huginn-mariadb
        environment: 
            - HUGINN_DATABASE_HOST=huginn-mariadb
            - HUGINN_DATABASE_PORT=3306
            - HUGINN_DATABASE_NAME=huginn
            - HUGINN_DATABASE_USERNAME=huginn
            - HUGINN_DATABASE_PASSWORD=123456
            - SMTP_SERVER=mail.233.fi
            - SMTP_PORT=587
            - SMTP_USER_NAME=imlala@233.fi
            - SMTP_PASSWORD=123456
            - EMAIL_FROM_ADDRESS=imlala@233.fi
        ports:
            - 3000:3000
        restart: unless-stopped
    huginn-mariadb:
        image: mariadb
        container_name: huginn-mariadb
        environment: 
            - MYSQL_DATABASE=huginn
            - MYSQL_USER=huginn
            - MYSQL_PASSWORD=123456
            - MYSQL_ROOT_PASSWORD=123456
        volumes: 
            - ./db:/var/lib/mysql
        restart: unless-stopped
```

“终端” 输入：

```
docker-compose up -d
```

部署结束后，在浏览器地址栏输入 “服务器 IP:3000” 并访问，显示页面就表示部署成功。默认的账户名是 admin，密码是 password。

**2.2 新建第一个 Agent，抓取网页信息**

登入 huginn 后，点击 Account→修改一下邮箱、密码。

![](https://img.yanzhihome.com/huginn%20%E6%94%B9%E5%AF%86%E7%A0%81-16515829145954.png)

点击页面上方的 Agents →New Agents 创建新任务。

![](https://img.yanzhihome.com/image-20220503002233643.png)

**Type**：选择 Website Agent；**Name：**填入项目、网站名；**Schedule**：选择抓取内容的更新频率。

![](https://img.yanzhihome.com/image-20220503001859051.png)

Options 代码区，在”url” 后填入抓取网站的链接，”mode” 后填入 on_change。

在 chrome 内核浏览器中，打开网站链接，右键点击页面选择 “检查”（或者按 F12），右键点击选择要抓取的元素，审查元素面板会定位到该节点，右键点击该元素节点→复制→复制完整 Xpath。

![](https://img.yanzhihome.com/image-20220503001038117.png)

然后在 huginn 界面 options→extract→url→“xpath”后填入复制好的 Xpath 节点路径 (li 后面的“[1]” 标签需要删除，因为不是只抓第一个 li, 而是整个列表），在 “url” 的”value“后填入 @href 提取链接；

![](https://img.yanzhihome.com/image-20220503000346403.png)

“title” 也是一样，填入复制好的 Xpath 节点路径，”value“后填入 string(.) 提取节点路径下的所有字符串，或者 normalize-space(.) 来提取去除多余空格的字符串。也可以选择其他的如./node()、text() 来测试看看效果。

添加一个与 extract 平级的 template 链接补全模板，url 后填入：“抓取的网址链接”＋“{{url}}”。

![](https://img.yanzhihome.com/image-20220503000225264.png)

最后点击 Dry Run 看看抓取效果。

![](https://img.yanzhihome.com/image-20220503210532528.png)

**2.3 创建第二个 Agent，生成 RSS 地址**

**Type**：选择 DataOutputAgent；**Name：**填入项目、网站名；**Schedule**：选择抓取内容的更新频率；**Sources：**选择第一个 Agent。

![](https://img.yanzhihome.com/image-20220503213152942.png)

配置 Options，title 填入 RSS 名，link 填入抓取页面的网址，item 的 title、link 等项，填入 {{title}}、{{url}}。

![](https://img.yanzhihome.com/image-20220503214529866.png)

点击 Save 保存 Agent，就可以用显示的 xml 地址，去 RSS 阅读器订阅该网站了。

![](https://img.yanzhihome.com/image-20220503214914617.png)

二、订阅推特

自建 RSSHub 玩家，如果网络上找的镜像域名失效，也可以用 [https://twiiit.com/](https://twiiit.com/) 这样的推特镜像网站，在推特用户页面，获取订阅源。

![](https://img.yanzhihome.com/image-20220429223901344.png)

三、订阅 Instagram
--------------

同上，也可以用 [Bibliogram](https://bibliogram.art/) 烧制订阅源。

![](https://img.yanzhihome.com/image-20220429224332993.png)

四、订阅 Newsletter
---------------

可以使用 [Kill the Newsletter! (kill-the-newsletter.com)](https://kill-the-newsletter.com/) 服务生成的邮箱去订阅 Newsletter。

![](https://img.yanzhihome.com/image-20220429231403779.png)

![](https://img.yanzhihome.com/image-20220429231801342.png)

五、订阅微博
------

[Weibo to RSS](https://rssfeed.today/weibo/)

![](https://img.yanzhihome.com/image-20220507233439236.png)

六、订阅源过滤
-------

**siftrss.com**

支持标题包含或排除关键词，

![](https://img.yanzhihome.com/image-20220503221550818.png)

支持正则表达式过滤（”/ 关键词 | 关键词 | 关键词 / i”，可以用 “shift+\” 打出”|“符号）。

![](https://img.yanzhihome.com/siftrss-16515875416985.png)
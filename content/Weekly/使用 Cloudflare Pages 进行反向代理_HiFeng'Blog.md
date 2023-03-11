> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.hicairo.com](https://www.hicairo.com/post/59.html)

> Cloudflare Pages, 反向代理, Cloudflare,CF,CDN,Cloudflare Workers,pages.dev,workers.dev, 没有域名使用 CF

最近群里几位大佬为大家分享了好几个容器的使用方法，例如 [Replit](https://www.hicairo.com/post/53.html) 、[Doprax](https://www.hicairo.com/post/55.html) 、Deepnote 等。在使用过程中，要么平台分配的域名被墙，要么速度不稳定，需要配合 Clondflare CDN 使用。但是 Clondflare Workers 分配的域名已被污染，鉴于有些小伙伴没有域名，今天就为大家分享使用 Cloudflare Pages 进行反向代理的方法。

**一、使用条件**

需要有 Github 及 Clondfiare 的账号。

**二、在 Github 上建立仓库并添加代码**

1、登录 [Github](https://github.com/) 后，如下图所示，建立一个名为 Cloudflare Pages 的私库。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675923922290032.webp)

2、点击 creating a new file 按钮，创建文件。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675923938666899.webp)

3、创建一个名为 **_worker.js** 的文件，然后保存。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675923954837769.webp)

用你需要反代的域名 (平台分配被墙的域名) 替换第 5 行中的 www.hicairo.com 。  
注意：域名中不要加 https,http 等字符。

```
export default {
  async fetch(request, env) {
    let url = new URL(request.url);
    if (url.pathname.startsWith('/')) {
      url.hostname = 'www.hicairo.com'
      let new_request = new Request(url, request);
      return fetch(new_request);
    }
    return env.ASSETS.fetch(request);
  },
};
```

**三、在 Cloudflare 中设置 Cloudflare Pages**   

1、登录 [Cloudflare](https://www.cloudflare.com/) ，点击左侧菜单中的 Pages 按钮后，然后点击页面右侧的 Create a project 按钮。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675923973780042.webp)

2、点击页面右侧的 Connect to Git 按钮。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675923989305998.webp)

3、选择 GitHub 后点击 Connect to GitHub 按钮。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675924003406797.webp)

4、页面跳转至 Github ，点击 Install & Authorize 按钮。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675924016103924.webp)

5、页面跳转回 Cloudflare ，选择你刚才创建名为 Cloudflare Pages 的仓库，然后点击 Begin setup 按钮继续。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675924030799170.webp)

6、Project name 可以使用默认，也可以随便填写，然后点击页面底部的 Save and Deploy 按钮。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675924043209975.webp)

7、等待部署完成后，页面中会出现如图示内容，其中显示的域名就是 Cloudflare Pages 平台为你分配的域名，*.pages.dev 域名目前还没有被污染，通过该域名可以正常打开您的站点。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302091675924054725802.webp)

**四、添加自定义域名**

由于 pages.dev 域名在某些地区已被污染，添加自定义域名是必要的。前提是你已拥有一枚域名，并托管在 Cloudflare 。如何将域名托管在 Cloudflare ，请参考《[V2ray 使用 Cloudflare 中转流量，拯救被墙的 IP](https://www.hicairo.com/post/24.html)》第五章节，本文不再赘述。

1、点击页面左侧菜单中的 Pages ，然后在页面右侧点击刚才创建好的项目名称。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302141676342153674132.webp)

2、点击 Custom domains ，然后点击 Set up a custom domain 按钮，添加自定义域名。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302141676342170603735.webp)

3、填入域名然后点 Continue 按钮。例如：我在 Cloudflare 上托管了的域名为  ifeng.ml, 我添加的自定义二级域名 example.ifeng.ml 。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302141676342180205448.webp)

4、点击 Activate domain 按钮。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302141676342191706719.webp)

5、等待 Initializing 完成，域名 Verifying 完成后，会出现 Active 字样。这时说明自定义域名已经设置成功了，你可以使用自定义域名访问你的站点。这一步正常情况下需要 1-2 分钟时间。

![](https://www.hicairo.com/zb_users/upload/2023/02/202302141676342202295211.webp)

本文出处：HiFeng'Blog  
本文链接：[https://www.hicairo.com/post/59.html](https://www.hicairo.com/post/59.html)  
版权声明：本博客所有文章除特别声明外，均采用 [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh) 许可协议。转载请注明出处！
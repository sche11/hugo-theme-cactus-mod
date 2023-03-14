> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.mjyai.com](https://blog.mjyai.com/2021/01/31/how-to-contribute-rsshub/)

> 官方文档简洁清晰，再增加内容就显得臃肿了。故另外写一篇对新手友好的指南。

发表于 2021-01-31|更新于 2022-10-22|[笔记](https://blog.mjyai.com/categories/%E7%AC%94%E8%AE%B0/)

| 阅读量:

官方文档简洁清晰，再增加内容就显得臃肿了。故另外写一篇对新手友好的指南。

万物皆可 RSS，这个项目是一个将任意网页内容转换为 RSS 的框架。其开源性质其实是鼓励大家按个人需求自己动手写规则的。

有的网站是有提供 RSS 的，如果你只是需要全文输出可以结合 [full-text-rss](https://blog.mjyai.com/2020/03/23/ubuntu-full-text-rss/) 来实现。  
有的网站已经有 RSSHub 规则了，可以通过 [RSSHub Radar](https://github.com/DIYgod/RSSHub-Radar) 或 [RSSBud](https://github.com/Cay-Zhang/RSSBud) 快速发现和订阅。

Fork 然后将你的项目`git clone`到本地。  
给你的项目增加上游：

```
git remote add upstream https://github.com/DIYgod/RSSHub
```

若以前已贡献过则需要从上游获取最新内容并强制更新：

```
git fetch upstream
git reset --hard upstream/master
git rebase upstream/master
git push -f origin master
```

推荐用 [Node Version Manager](https://github.com/nvm-sh/nvm) 灵活切换 npm 版本。

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

重启终端然后安装 npm 的稳定版：

```
nvm install stable
```

国内环境则推荐改为淘宝源（可选）：

```
npm config set registry https://registry.npm.taobao.org
```

通过`npm config get registry`可检查是否更改成功。

进入项目根目录。

```
npm install
npm run dev
```

然后浏览器打开`http://localhost:1200`。`dev`模式下每次保存项目就会自动重启应用修改，方便实时调试。

这里以[网易号（通用）](https://github.com/DIYgod/RSSHub/pull/6748)为例解释如何添加新规则。  
网易对大部分网易号是提供了 api 调取文章列表的，但有些网易号搜索页面搜不到的小众网易号（文章页面不含`data-wemediaid`）无法用 api 获取网页列表。  
比如这个[后厂村体工队](https://www.163.com/dy/media/T1555591616739.html)。

[](#添加脚本路由 "添加脚本路由")添加脚本路由
--------------------------

打开`/lib/router.js`，增加路由。

```
router.get('/netease/dy2/:id', require('./routes/netease/dy2'));
```

由前面网易号的主页可见，其链接最后 html 的文件名可用于区分网易号，故作为参数`id`传入脚本。若是可选参数则是`:param?`这样的格式。

[](#编写脚本 "编写脚本")编写脚本
--------------------

在 `/lib/routes/`中的路由对应路径下创建新的 js 脚本。由前面路由可见新建`dy2.js`。

### [](#import所需模块 "import所需模块")import 所需模块

```
const got = require('@/utils/got');
const cheerio = require('cheerio');
const iconv = require('iconv-lite');
```

这里`got`用来获取 html 信息，`cheerio`处理获取的数据。由于某些网易页面并不是用通用的`utf8`编码，故还需要`iconv-lite`进行格式转换。

### [](#获取主页数据并生成文章列表 "获取主页数据并生成文章列表")获取主页数据并生成文章列表

优先用 api 方式获取，但由前所述此法不可行。故直接抓取主页信息。另外还有一种方法是使用`puppeteer`渲染页面，这里不涉及。

```
const id = ctx.params.id;

const url = `https://www.163.com/dy/media/${id}.html`;

const response = await got.get(url, { responseType: 'buffer' });

const data = iconv.decode(response.data, 'gbk');

const $ = cheerio.load(data, { decodeEntities: false });


const list = $('.media_articles ul li')
    
    .slice(0, 5)
    
    .map((_, item) => {
        item = $(item);
        
        const a = item.find('h2.media_article_title a');
        
        let pubDate = item.find('.media_article_date').text();
        pubDate = new Date(pubDate).toUTCString();
        
        return {
            title: a.text(),
            link: a.attr('href'),
            pubDate: pubDate,
        };
    })
    .get();
```

具体如何用浏览器选择可见[这节图文教程](https://blog.mjyai.com/2020/12/22/raspberry-pi-docker-webmonitor/#%E6%B7%BB%E5%8A%A0%E7%BD%91%E9%A1%B5%E7%9B%91%E6%8E%A7%E4%BB%BB%E5%8A%A1)。

### [](#遍历文章列表并抓取全文 "遍历文章列表并抓取全文")遍历文章列表并抓取全文

```
const items = await Promise.all(
    list.map(async (item) => {
        let content;
        
        if (item.link.startsWith('https://www.163.com')) {
            
            const itemData = await ctx.cache.tryGet(item.link, async () =>
                iconv.decode(
                    (
                        await got.get(item.link, {
                            responseType: 'buffer',
                        })
                    ).data,
                    'gbk'
                )
            );
            content = cheerio.load(itemData, { decodeEntities: false });
        
        } else {
            const itemData = await ctx.cache.tryGet(
                item.link,
                async () =>
                    (
                        await got.get(item.link, {
                            responseType: 'buffer',
                        })
                    ).data
            );
            content = cheerio.load(itemData, { decodeEntities: false });
        }

        
        const eDescription = content('.post_body').html();

        
        const single = {
            title: item.title,
            link: item.link,
            description: eDescription,
            pubDate: item.pubDate,
        };
        return Promise.resolve(single);
    })
);
```

注：网易原来有部分网址是 gbk 编码的，现在全部改成 utf-8 了，处理更方便。更新代码见[此处](https://github.com/mjysci/RSSHub/blob/8789646b4783233c332fdc8024e9ebaf9c699720/lib/routes/netease/dy2.js)。

```
let link;
ctx.state.data = {
    title: $('.media_info h1').text(),
    link,
    description: '',
    item: items,
};
```

[](#添加脚本文档 "添加脚本文档")添加脚本文档
--------------------------

更新`/docs/`目录内对应的文档，可以执行`npm run docs:dev`查看文档效果。  
这里网易号属于新媒体，故修改`/docs/new-media.md`。

```
## 网易号（通用）
<Route author="mjysci" example="/netease/dy2/T1555591616739" path="/netease/dy2/:id" :paramsDesc="['id，该网易号主页网址最后一项html的文件名']" anticrawler="1"/> 
优先使用方法一，若是网易号搜索页面搜不到的小众网易号（文章页面不含`data-wemediaid`）则可使用此法。
触发反爬会只抓取到标题，建议自建。
```

格式是`markdown`。其中`:paramsDesc`是通过数组解释路由中每个参数的作用和获取方式，其他项不言自明，参考这个例子填写即可。

[第三方 RSSHub](https://github.com/AboutRSS/ALL-about-RSS#rsshub)，对于反爬严格的网站还是推荐[自建服务](https://docs.rsshub.app/install/#docker-compose-bu-shu)。

[提交新的 RSSHub 规则](https://docs.rsshub.app/joinus/#ti-jiao-xin-de-rsshub-gui-ze)  
[RSSHub 文档](https://docs.rsshub.app/)
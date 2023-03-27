> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.tjsky.net](https://www.tjsky.net/tutorial/644)

> 随着订阅源增多，再怎么说英语也不是日常语言，获取信息的速度明显不如中文， 况且慢慢地有俄语，韩语等语言的订阅源，就完全看不懂了，产生了翻译 RSS 的需求。

随着 RSS 订阅源越来越多，从非中文 RSS 订阅源获取消息就出了点问题，  
英文站点不多的时候，看原始文章标题还是没感到什么阻碍的。所以并没有使用到翻译。  
随着订阅源增多，再怎么说英语也不是日常语言，获取信息的速度明显不如中文，  
况且慢慢地有俄语，韩语等语言的订阅源，就完全看不懂了，产生了翻译 RSS 的需求。  
在一番寻找下，最终找了一个基于 GitHub Action + Google Translate 实现翻译 RSS 订阅源全文的项目。

![](https://img.tjsky.net/2023/03/d8b1e2c463af1f764cb79b87252e2065.png)

需要准备的东西
-------

这次你只需要准备一个 github 账号。  
注册地址（[https://github.com/signup](https://www.tjsky.net/goto/?url=https://github.com/signup "https://github.com/signup")）  
输入邮箱地址和密码，选择免费计划，验证邮箱地址，按照提示操作，创建您的个人帐户。  
PS：如果你感觉部分内容是英文的识别困难，用浏览器的翻译功能吧。

GitHub 部署
---------

### 记录三个需要的参数

#### U_NAME

就是你 github 的用户名，你可以点右上角的头像看到一行字：  
`Signed in as xxxxxx`，这个 xxxx 就是你的用户名

#### U_EMAIL

就是你 github 的注册邮箱，如果你实在是记不清了，可以点右上角的头像  
Settings→Access→Emails，然后右侧就会看到你的邮箱了

#### WORK_TOKEN

因为项目涉及使用脚本操作仓库内容，所以需要给脚本修改仓库内文件的权限，需要申请一个 Repository Secret 令牌。  
1. 点击网页右上角自己的头像，点 【Settings】  

![](https://img.tjsky.net/2023/03/29f6cfe81bc03557aedad19abdb33919.png)

2.  点击左侧最下方的【Developer settings】  
    ![](https://img.tjsky.net/2023/03/4e47a98edffdf66b38be46a4c0232a70.png)
3.  点击左侧下方的【Personal access tokens】-【Tokens(classic)】 ，点击左上角的 【Generate new token （classic）】新建一个 token  
    
    ![](https://img.tjsky.net/2023/03/9bf2fe1b0b54cb2c352896aae71d83b4.png)
    
4.  新建 token
    

*   Note: rss translate
*   Select scopes: 勾选【repo】和【workflow】（你直接勾 workflow，repo 就全勾上了）
*   Expiration：选【No expiration】（无期限）
*   点击页面最下方的 【Generate token】  
    ![](https://img.tjsky.net/2023/03/ffacdb28656d9482de3dd0c9d265bc06.png)

5.  复制 token  
    **注意一定要在这里复制好，错过这个页面你就再也看不到 token 了。**  
    **注意一定要在这里复制好，错过这个页面你就再也看不到 token 了。**  
    **注意一定要在这里复制好，错过这个页面你就再也看不到 token 了。**  
    
    ![](https://img.tjsky.net/2023/03/2ad554b2adc04cb6dfad17b25620d388.jpeg)
    
6.  返回你 repo 的 Upptime 项目。点击 【Settings】，展开左侧的【Secrets】，点击【Actions 】 点击【 New repository secret】  
    
    ![](https://www.tjsky.net/wp-content/uploads/2022/09/20220920114206.png)
    

### Fork 项目

1.  登录你的 Github，并且进入项目（[https://github.com/tjsky/RSS-Translation](https://www.tjsky.net/goto/?url=https://github.com/tjsky/RSS-Translation "https://github.com/tjsky/RSS-Translation")）
2.  点击右上角的【Fork】将项目复刻到你自己的仓库

### 设置需要的令牌

点击 【Settings】，展开左侧的【Secrets and varlables】，点击【Actions 】 点击【 New repository secret】

![](https://img.tjsky.net/2023/03/e9720df9254aa203bc5e2b95cad0d64d.png)

*   给翻译仓库设定 U_NAME 参数
    *   Name: U_NAME
    *   Value: 上边 U_NAME 所说的你的用户名
    *   点击 【Add secret】
*   给翻译仓库设定 U_EMAIL 参数
    *   Name: U_EMAIL
    *   Value: 上边 U_EMAIL 所说的你的邮箱
    *   点击 【Add secret】
*   给翻译仓库设定 WORK_TOKEN 参数
    *   Name: WORK_TOKEN
    *   Value: 上边 WORK_TOKEN 所说的你的令牌
    *   点击 【Add secret】

### 给需要的权限

1.  给与 actions 读写权限
    *   点击 【Settings】，展开**左侧的**【Actions】
    *   点击【General 】 找到【 Workflow permissions】
    *   将选项改为【Read and write permissions】
    *   点击 Save 按钮。
2.  开启 GitHub Pages
    *   点击【Settings】
    *   在左侧 【Code and automation】 下找到 【Pages】 点击进入
    *   将 【Branch】 设置为 【main】
    *   点击 【Save】

1.  点击【Code】，点击进入【 test.ini 】文件  
    ![](https://img.tjsky.net/2023/03/dc8bc11a29bc340677dd8f33a1a3e12e.png)
2.  点击笔形图标，编辑代码  
    
    ![](https://img.tjsky.net/2023/03/c0738797871caa159c7e5e339ea80f0c.png)
    
3.  设置你需要的订阅源  
    前两行的内容不要动。
    

需要改 RSS 订阅源请改后面的代码，格式如下

*   `[source001]`：订阅序号，从 001 开始增长，注意请确保编号不要重复，不然代码会报错
*   `name = "mckinsey_rss.xml"`：生成订阅的名称，只允许包含英文字母（a-zA-Z）、数字（0-9）、(`-`,`_`,`.`,`~`)4 个特殊字符, 并且结尾一定是. xml 或. rss
*   `url = "http://www.mckinsey.com/insights/rss"`：RSS 订阅链接  
    –`max = "10"`：每次 RSS 订阅源获取的更新条数，如果你的订阅源为全文订阅（就是会显示一大堆文字的话），请适当减少这个数字的大小，因为脚本使用的翻译接口，有最大字符数限制，一次更新太多（翻译太多）会导致后面的文字没有被翻译。
*   `md5 = ""`：留空即可，将来脚本会自己计算这个数字写入
*   `action = "auto"`：翻译方向，设置为 auto 会将任意文字翻译为中文，如果想指定可以看这个  
    [源语言](https://www.tjsky.net/goto/?url=https://pygtrans.readthedocs.io/zh_CN/latest/source.html "源语言") -> [目标语言](https://www.tjsky.net/goto/?url=https://pygtrans.readthedocs.io/zh_CN/latest/target.html "目标语言")。比如：`en->zh-CN`意思就是从英语翻译为中文简体。

4.  点击最下边的【Commit changes】提交修改。

### 测试翻译

![](https://img.tjsky.net/2023/03/5a8e778b4f72da33c3045e71b4fc6e0e.png)  
– 点击 【Actions】  
– 点击【circle_translate】  
– 选择 【Run worldiow】  
– 你会看到 1~2 个黄圈圈在转。运行成功会显示绿色的勾，运行失败会显示红色的叉。如果出现红叉，一般都是你修改 ini 文件时，什么地方写错了, 权限、令牌设置错误，比如少打了一个 字母啊，空格漏了啊，代码对齐有问题，少写了什么必须设置的参数，什么参数设置错误了。请仔细检查。

### 修改运行参数

1.  点击【Code】，点击进入【 README.md 】文件  
    ![](https://img.tjsky.net/2023/03/dc8bc11a29bc340677dd8f33a1a3e12e.png)
2.  点击笔形图标，编辑代码  
    
    ![](https://img.tjsky.net/2023/03/c0738797871caa159c7e5e339ea80f0c.png)
    
3.  将 5/6/8/10 这 4 行中，一切你看到的`tjsky`改成你自己 github 用户名（就上边所说的 U_NAME）
    
4.  点击最下边的【Commit changes】提交修改。
    

如果前边没出现错误（主要是 actions 上没出现红叉），那么你可以在你自己项目的介绍页，看到这样的内容  

![](https://img.tjsky.net/2023/03/d8b1e2c463af1f764cb79b87252e2065.png)  
点击那个【查看 XXXXXXX】链接，就可以跳转到订阅列表页，其他就可以一帮的 RSS 订阅一样了。

注意
--

*   这个项目纯属娱乐，因为很多网站的 RSS 订阅格式并不是很规范（当然这个也不赖网站，因为 RSS 本身就是一个非常混乱的标准）不排除会出现，翻译后的 RSS 翻译订阅源，阅读器报错无法使用的情况。
*   尽量不要翻译那种全文显示的订阅源（比如 RSSHUB 生成的那种）字数太长翻译很容易出错，如果因为过长出错，请对应减少`max = " "`参数的数字。
*   默认设置是每 2 小时所有拉取一次订阅源并翻译，如果需要改的更短请修改`.github/workflows/circle_translate.yml`文件第 7 行，比如

<table><thead><tr><th>内容</th><th>时间</th></tr></thead><tbody><tr><td>– cron: ‘0 */2 * * *’</td><td>每 2 小时运行一次</td></tr><tr><td>– cron: ‘0 * * * *’</td><td>每 1 小时运行一次</td></tr><tr><td>– cron: ‘*/30 * * * *’</td><td>每 30 分钟运行一次</td></tr></tbody></table>

因为 github actions 的设计，运行时间会根据 github 本身负载调整，实际更新间隔会略有加长，比如你设定 1 小时运行一次，实际可能是 1 小时 7 分钟间隔，1 小时 3 分钟间隔。
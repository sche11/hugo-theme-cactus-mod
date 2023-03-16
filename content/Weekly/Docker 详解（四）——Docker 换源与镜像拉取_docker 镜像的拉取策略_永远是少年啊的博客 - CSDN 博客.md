> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_40228200/article/details/124156331)

今天继续给大家介绍 [Linux 运维](https://so.csdn.net/so/search?q=Linux%E8%BF%90%E7%BB%B4&spm=1001.2101.3001.7020)相关知识，本文主要内容是 Docker 的换源与镜像拉取。

一、Docker 镜像源配置
--------------

Docker 在安装后，我们需要前往 Docker Hub 上拉取（及时就是下载的意思）镜像。但是，由于网络的原因，我们在 Docker Hub 上拉取镜像时网速很慢，这时，我们就需要换 Docker 的镜像源，换成我们国内的 Docker 镜像源，以方便我们 Docker 镜像的拉取。  
在这里，我以阿里云的 Docker 镜像源为例，进行 Docker 更换镜像源的配置。  
首先，我们访问阿里云，网址为 [https://www.aliyun.com/](https://www.aliyun.com/)，并进行登录。登录后进入 “控制台”，然后选择如下所示的 “容器镜像服务”。  

![](https://img-blog.csdnimg.cn/0e243dd5bc91437389f129a518819ca8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5rC46L-c5piv5bCR5bm05ZWK,size_20,color_FFFFFF,t_70,g_se,x_16)  
在弹出的窗口中，选择 “镜像加速器”，右边会出现配置说明。  
![](https://img-blog.csdnimg.cn/1d94770b3a394d888c502e023623cc68.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5rC46L-c5piv5bCR5bm05ZWK,size_20,color_FFFFFF,t_70,g_se,x_16)  
我们按照说明，打开 / etc/docker/daemon.com 文件，并写入该镜像加速器所指定的内容，该文件配置完成后如下所示：  
![](https://img-blog.csdnimg.cn/c657fe461cd44dbc9180b400dec4f16d.png)  
之后，我们执行命令：

```
systemctl daemon-reload
systemctl restart docker
```

以使得我们的镜像源生效。

二、Docker 镜像下载
-------------

在 Docker 的镜像源配置之后，接下来，我们就可以开始进行 Docker 的镜像下载了。  
首先，我们执行命令：

```
docker search centos
```

可以搜索所有有关 CentOS 系统的镜像，结果如下所示：  

![](https://img-blog.csdnimg.cn/350261eba30d4dd0a870f6c27f9874bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5rC46L-c5piv5bCR5bm05ZWK,size_20,color_FFFFFF,t_70,g_se,x_16)  
在搜索结果中，我们可以看到有 6 列信息。其中，第一列为镜像索引，第二列为镜像名称，第三列为镜像描述，第四列为镜像的星星数量，反应处了镜像的受欢迎程度，第五列标识了该镜像是否为官方镜像，第六列表示是否为自动构建的镜像。  
我们选择好我们需要的镜像，执行命令：

```
docker pull 【镜像名称】
```

即可完成指定镜像的下载，例如：  
执行命令：

```
docker pull docker.io/centos
```

即可将该镜像下载到本地，如下所示：  

![](https://img-blog.csdnimg.cn/03f7552ae75549b691409e854d32874a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5rC46L-c5piv5bCR5bm05ZWK,size_20,color_FFFFFF,t_70,g_se,x_16)  
之后，我们执行命令：

```
docker images
```

即可查看当前的镜像，如下：  

![](https://img-blog.csdnimg.cn/ffa2a34bb5bd424b8868e6b127a3a689.png)  
原创不易，转载请说明出处：https://blog.csdn.net/weixin_40228200
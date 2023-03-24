> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [mp.weixin.qq.com](https://mp.weixin.qq.com/s?__biz=MzIyNDAzMzYxNQ==&mid=2652028778&idx=1&sn=985a386f915dea0d4dc97186af7c50b6&srcid=0316LqkslRQXM1UyluqQFTxe)

最近看到好多基于 OpenAI API 接口的 AI 应用，是春天到了，如雨后春笋般冒出来了。ChatGPT 输入有 4096 token 的限制，也就是一次问答提问和返回的字数有限， 而且所有回答都是基于 2021 年前的互联网信息。这个就不太友好了，至少有两方面急需改进下， 一是实时性，二是内容定制化。实时性现在 New Bing 做得不错。定制化的问答很常见的使用场景就是做特定领域的知识库，给它投喂特定的知识，把它训练成想要的问答机器人。比如知识产权律师事务所要对外提供一个法律顾问的机器人，让它能回答常见的法律咨询，能结果律所已有的案例答复。机器人可以近乎无限扩展的方式来提升效率，降低人工费用。用它预接待客户或者引流是可以想到的使用场景。我相信 GPT3.5 是可以做到的。

现有的公开服务
=======

这里列出几个，使用方法都很相似：上传文档，服务器分析文档，然后用户提问，服务器返回基于文档的回答。

*   https://chatpdf.com
    
*   https://www.pandagpt.io/
    
*   https://chat2doc.cn
    
*   … 后面会有试用 chatpdf 的体验。
    

寻求建议
====

有了想法，但不知道如何实施。没关系，直接问 ChatGPT 和 New Bing. 这是 prompt

> there is a website chatpdf.com that parses your uploaded pdf document and serve any question related to the document content. It is based on OPEN AI API. How can I build such website? Could you please give me more detail on “create knowledge base with open ai embeddings”, I want sample code that I can follow. Thanks

看到 ChatGPT 的回复，思路立马打开了。

![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27XgyviaRqzO9AYSRmL2pTiciaHrpOl6Xp5oetOgCUPuYTNks6k29Zye63qg/640?wx_fmt=png)

使用 Llama_Index 包
================

> LlamaIndex 是一个基于文本嵌入（text embedding）的近似最近邻搜索引擎。它可以将文本数据集编码为低维向量，并利用这些向量来快速查找与查询向量最相似的数据点。LlamaIndex 可以支持多种文本编码方法，例如基于深度学习的词嵌入（word embeddings）和基于类似于 Locality Sensitive Hashing（LSH）的方法进行的编码。LlamaIndex 的设计旨在支持大规模文本数据集的高效搜索。---- from ChatGPT

看不太懂。说人话， LlamaIndex 是一种可以快速搜索相似文本的工具。它可以把很多文本拆分，变成一些数字，建立索引，然后比较这些数字的相似度，找到最相似的那些文本。这个工具可以帮助我们在海量的文本中快速找到我们感兴趣的内容。

以前它叫 GPT Index，感兴趣可以查看：https://github.com/jerryjliu/llama_index

这里有一个跑在 colab 上的 Demo (Jupter 脚本), 里面有比较详细的说明，点开登陆 google 直接一步步跑吧。https://colab.research.google.com/drive/11WDzga57dXaW-O7tq9GpaXHisDYOz3zx?usp=sharing

最后能实现有问有答，但效果并不是太好，还有许多微调的工作要做。

![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27XFibz32eabYtvuQS9ydWhiavSibqMqBVVLBgAoE5HKHCnnfWgJVey3fbJg/640?wx_fmt=png)

使用 ChatPDF
==========

拿常看的科技爱好者周刊来测试

1.  准备数据 因为 chatpdf 对免费用户有一定限制（文档 5MB，120 页），所以先处理一下 markdown 文件，尽可能保留文本信息。
    

```
git clone https://github.com/ruanyf/weekly.gitcd weekly/docscat issue-2??.md > weekly.mdsed -i '/^$/d' weekly.mdsed -i 's/^[[:space:]]*//' weekly.mdsed -i '/^!\[\]/d' weekly.mdsed -i '/## 回顾/,/（完）/d' weekly.mdsed -i '/<iframe/,/<\/iframe>/d' weekly.mdsed -i 's/(https[^)]*)//g' weekly.mdsed -i 's/[][]//g' weekly.md
```

2.  转换为 PDF 追求格式完美的话用 pandoc 但其实只要文本信息，可以直接 VSCode 打开，安装插件 "Markdown PDF", 然后按 F1, 输入 “Export(pdf)”，点击跳出来选项，就会在同一文件夹下生成同名的 PDF 文件。
    
3.  上传文档到 chatpdf.com
    
4.  根据上传的 200-245 期内容，提问过程如下。总的来说，提问如果与文档内容关联度高，它会返回比较正确的答案，但也会根据自己的理解修改答案。如果文中没有相关信息，它会以自己原有的知识库编内容。有的没大错，比如说阮老师对硅谷银行的观点。有的就是胡扯，说老师有离婚经历。
    

![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27XATWlOUBC1qSgabtoHibOxjjZW7icIIriak5bVicxo86T1v3py23soIXD0g/640?wx_fmt=png)1![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27Xz34cQf4G5ic3m2c7jkQ8qlYqWdiaAeXXBmuEZib2Wg9vBuDt33cKN6vFA/640?wx_fmt=png)2![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27XrSocpmyyoWQP8UKbRlzib1quiarECFmgfmmT7PtQDsHGlgrwb0Gmao7Q/640?wx_fmt=png)3![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27XlLC84y9liaUU6arG43EcJGVXZYFpuneKqESDX04c9R9UzJv9lQ5QRGw/640?wx_fmt=png)4![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27XD3tB3kbFgRS5gXpruwfUOj0BC5SsicoOmohG2NLtoJ5ibQaLRYVIdQ6A/640?wx_fmt=png)5![](https://mmbiz.qpic.cn/mmbiz_png/VXdFUnbrlOhuVhkrTSq7l5rnpWmsE27XOy1THKibvwAcOYvX5dFKAZGWxcWfMygiaM9zf3Z2qrAq8TiciaHCSm4ibtg/640?wx_fmt=png)6

思考
==

ChatGPT API 还只是大语言模型，本质上是它会处理语言信息。但不会完全像人一样处理语言信息，还有一些不太完善的地方，但已够惊艳。**如果知识库的回答如果不可信，那还需要它吗？**历史告诉我们，不要刻舟求剑，AI 的发展超出想象。今天发布的 GPT 4.0，已经不只是个大语言模型了。后面的 5.0, 6.0 的逻辑能力，总结，洞察能力会飞速提升。要是再带上个性，情绪，要是全世界一起调教它，它产生了对创意的认识，对道德的评判，甚至有了自主意识都是有可能的。对未来不要悲观吧，希望制造它们的人们能理智一点，也约束一点。
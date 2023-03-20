> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.mjyai.com](https://blog.mjyai.com/2023/03/18/run-meta-chatgpt-llama-using-cpu/)

> Meta 推出了开源的 LLaMA，本篇介绍 CPU 版的部署方式，依赖简单且无需禁运的 A100 显卡。

Meta 推出了开源的 LLaMA，本篇介绍 CPU 版的部署方式，依赖简单且无需禁运的 A100 显卡。  

OS: Ubuntu 22.04

CPU: Ryzen 5 5600X

官方的 [LLaMA](https://github.com/facebookresearch/llama) 需要大显存显卡，而魔改版的 [llama.cpp](https://github.com/ggerganov/llama.cpp) 只需大内存即可。

```
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp
make
```

我用的是 conda 进行 python 环境管理，[如何安装 conda](https://blog.mjyai.com/2020/01/24/rtorrent-compile/)。

创建并激活环境

```
conda create -n pt-cpu python=3.10
conda activate pt-cpu
conda install pytorch torchvision torchaudio cpuonly -c pytorch sentencepiece
```

获取模型文件可通过[这里申请](https://forms.gle/jk851eBVbX1m5TAv5)，不想申请也有[捷径](https://github.com/facebookresearch/llama/pull/73/files)。

在项目根目录新建`models`文件夹，并把模型放进去，其结构如下：

```
models/
├── 13B
│   ├── checklist.chk
│   ├── consolidated.00.pth
│   ├── consolidated.01.pth
│   └── params.json
├── 30B
│   ├── checklist.chk
│   ├── consolidated.00.pth
│   ├── consolidated.01.pth
│   ├── consolidated.02.pth
│   ├── consolidated.03.pth
│   └── params.json
├── 65B
│   ├── checklist.chk
│   ├── consolidated.00.pth
│   ├── consolidated.01.pth
│   ├── consolidated.02.pth
│   ├── consolidated.03.pth
│   ├── consolidated.04.pth
│   ├── consolidated.05.pth
│   ├── consolidated.06.pth
│   ├── consolidated.07.pth
│   └── params.json
├── 7B
│   ├── checklist.chk
│   ├── consolidated.00.pth
│   └── params.json
├── tokenizer_checklist.chk
└── tokenizer.model
```

转换 7B 模型。

```
python convert-pth-to-ggml.py models/7B/ 1
./quantize.sh 7B
```

最后生成`ggml-model-q4_0.bin`。

转换 13B 模型。

```
python convert-pth-to-ggml.py models/13B/ 1
./quantize ./models/13B/ggml-model-f16.bin   ./models/13B/ggml-model-q4_0.bin 2
./quantize ./models/13B/ggml-model-f16.bin.1 ./models/13B/ggml-model-q4_0.bin.1 2
```

最后生成`ggml-model-q4_0.bin`和`ggml-model-q4_0.bin.1`。

注意 LLaMA 基于 GPT-3，但并不是像 ChatGPT（GPT3.5）那样的类 [InstructGPT](https://openai.com/research/instruction-following)——经过指示学习和人工反馈的强化学习的微调。所以并不能直接问问题，而需要合适的吟唱咒语。可参考官方的 [Prompt Tips](https://github.com/facebookresearch/llama/blob/main/FAQ.md#2-generations-are-bad)。

7B 模型：

```
./main -m ./models/7B/ggml-model-q4_0.bin -p "Simply put, quantum entanglement states that" -t 6 -n 512
```

内存占用约 4.7G。

13B 模型：

```
./main -m ./models/13B/ggml-model-q4_0.bin -p "Simply put, quantum entanglement states that" -t 6 -n 512
```

内存占用约 8.4G。

输出如下：

```
Simply put, quantum entanglement states that a pair of interacting particles can be described in terms as if the two were one single system or particle. This is what I mean by “entangled”:
Entangle two photons with each other and they will exhibit correlated behavior such that no matter how far apart they are, their actions affect (and are affected) instantaneously, even across vast distances in space-time . If we separate the entangles pair of particles spatially by some distance then any change to one particle’s state would be reflected with equal rapidity on its partner.
These two “entangled” photons can also interact and influence each other without being limited physically or electromagnetic in nature, meaning they do not have to share the same space-time coordinates (like a car wreck for example) nor are there any limitations imposed by distance between them; this means that information exchange could occur faster than light speed.
This is also known as quantum teleportation because of it’s ability to instantly transport the behavior or even matter across vast distances, although you can only move photons and not entire objects at once like a car wreck for example (those are called BH-entangled). This means that information exchange could occur faster than light speed.
Now here is where it gets really strange; because of the entangle two particles share their quantum state, no matter how far apart they may be in space and time at any given moment when one particle changes its behavior or goes through a change, then so does the other as if there were only “one” system interacting. If we separate these two systems by some distance from each others field of effect/influence (say for example: 1 light year apart) and they go their own ways to do something different than what was originally entangled, then at any moment the instantaneous change is reflected in both particles as if it were a “single system”.
This means that one particle has all of its information contained within itself but also includes a copy or replicate (if you will) of everything about every other subatomic constituent and elemental component inside another entangled pair; so to speak, the universe exists in multiples at once! It could be said that any given individual particle is not only an independent entity by definition it’s also like a hologram for all others because its entire history up until now will always remain part
```

说了一堆，遣词造句上没什么问题，但一眼就看出有个重大错误：纠缠的粒子对坍缩是超距的，但并不能利用这个来瞬时传信息，即信息的传输依然无法超越光速。

LLaMA 的训练集是 20 种语言的维基百科，并不包含中文，但我还是手贱试了下：

![](https://cdn.jsdelivr.net/gh/mjysci/imgs@master/blog/2023-03-18_23-29.png)

驴唇不对马嘴，不知所云还有错别字。

[FAQ](https://github.com/facebookresearch/llama/blob/main/FAQ.md)
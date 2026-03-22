
按顺序，笔记主分支还是 CS336，因为是个人笔记，中间会穿插各种延伸。


进入正题。第一课照常都是讲概论，把 LLM 里的几大块都带着走了一遍，没有什么侧重点。

总的来说，当前 LLM 研究可以用 SwiGLU 论文里的结论部分的一段话概括：
![[exp_conclusions.png]]
所以即便是 infra 笔记，我也更偏向于分享更多实验细节。

## 可拓展的算法才是好算法
Percy引用了 bitter lesson 里的观点：
>Wrong interpretation: scale is all that matters, algorithms don't matter.
>Right interpretation: algorithms that scale is what matters.
>**accuracy = efficiency x resources**

事实上，在更大规模下，效率要重要得多（无法承受资源浪费）。
核心思路：在给定算力与数据预算的前提下，能构建出的最优模型是最大化的效率。



# 分词器
本课唯一的核心知识点就是 tokenizer 分词器。

Karpathy 经常吐槽分词器这个设计是 LLM 最反直觉的一环，他认为分词是 LLM（大语言模型）中许多奇异现象的根源。即：

为什么 LLM 拼不对单词？分词。
为什么 LLM 无法完成像字符串反转这样的简单任务？分词。
为什么 LLM 在非英语语言（例如日语）上的表现更差？分词。
为什么 LLM 的简单算术能力很糟糕？分词。
为什么 GPT-2 在 Python 编程上比预期更困难？分词。
为什么 LLM 遇到字符串 "<|endoftext|>" 就突然停止了？分词。
为什么我会收到关于“尾随空格”的奇怪警告？分词。
为什么当我问 LLM 关于 "SolidGoldMagikarp" 时它会崩溃？分词。
为什么在与 LLM 交互时我应该优先选择使用 YAML 而不是 JSON？分词。
为什么说 LLM 不是真正的端到端语言建模？分词。
万物痛苦的真正根源是什么？分词。

下面我们来探讨分词的具体细节。
目前主流分词算法为
参考GPT2论文《Language Models are Unsupervised Multitask Learners》








经典的 bpe 分词器实现大概就是这些，但仅学到这总还是少了些什么，毕竟文本 bpe tokenizer 的实现算是老生常谈了。课程虽然也没提供更多材料了，但我希望更进一步：多模态是如何分词的？

>以下均为多模态 tokenizer 引申，可略过。

# Vision Encoder

将图像编码为视觉 token
VIT （参考 b站李沐 # ViT论文逐段精读【论文精读】这一期）



# Audio Encoder
语音信号相比于视频和文字更加连续，所以也更加麻烦。当前主流方法还是往离散信号上转，当然传统音频技术也是如此，只是近似连续。AudioLLM 这块做的更加彻底，我们假设这个世界上的声音在细粒度上存在某种重复性，即我们将每段语音切分成很多段固定长度的片段，再将这些片段归属到固定数量的种类中去（类似词表）

以李沐团队的 BosonAI 推出的 Higgs Audio 为例：
![[Pasted image 20260319163253.png]]

所以对于音频理解而言，核心在于语义的理解而不在于声义理解，大部分声音语调信息都在压缩中损失掉了，更多的保留了语义信息。


以 Higgs Audio 的 tokenizer 为例：
![[audio_tokenizer.png]]


```python
wadawd

```


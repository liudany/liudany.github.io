---

layout: post
title: Hierarchy Paragraph Generation
date: 2019-07-15 09:28:09
tags: [NLP]
categories: [NLP]
draft: true
---

## 之前代码存在的问题

- `zero-dimensional tensor cannot be concatenated`: `torch.cat((tracker['ELBO'], loss))`，在pytorch0.4以后loss变成了一个`0维tensor`，这是不同于数字的(但是可以和数字运算)，也不可以直接和1维tensor直接cat， 需要变成1维数组形式`loss.reshape(1)`或者`loss.unsqueeze(0)`的tensor再cat。

- 抛弃了`loss.data[0]`的用法，想要取数字而不将loss添加到多余的运算图，用`loss.item()`.
- Validate时显存爆炸，原因是validate时没有`loss.backward()`或者`optimizer.zero_grad()`的话就不能将计算图清空，但是之后有对于loss的***cat计算***，这样会一直积累loss的计算图，然后显存爆炸。更改的方法是在validate时将loss的计算后添加detach，即`loss = xxx.detach()`。detach()函数将一个变量从图中分离出来，分离出来的变量不需要梯度（计算图）。

## 存在的问题

- RNN-VAE中，输入和z在编码器和解码器里的应用？

- input_sequence是以`<sos>`开头，总长max_length，而target是是以第一个单词开头，以`<eos>`结尾，总长max_length。

pack_padded_sequence最主要的是记录`有用信息的长度`，再后来取输出的时候可以无视pad后的输出。

在transformer里面可能有这么几个问题：

1. 如果做到和rnn相同的pad处理方法，直接padding输入？

2. 怎么运用z这个向量，在rnn里面是做hidden_state输入的

3. rnn训练时候的解码阶段是直接解？

   可以作隐状态，可以每个time-step都concat，影响不大。

4. transformer解码阶段的mask怎么用？

5. transformer的inference阶段怎么一个词又一个词？

## 4/23-4/24

今天解决rnn到transformer的诸多过度问题，比如encoder后采样得到的z怎么输入到transformer中。这个问题反过来想在transformer当翻译模型的时候也会遇到，在decoder阶段怎么输入？所以先研究transformer解码过程。

1. 从复制任务来看，是encoder的输出直接全部放到decoder作为输入。

然后继续去读transformer代码了。

## 4/25

在RNN中，context vector是最后一个时间步的隐状态，然后映射到z，z再映射回来隐状态，再输入decoder_rnn中。
类比到transformer中，因为transformer是完全基于attention机制的，但是之前vae-rnn都是没有attention的，所以如何解决z和attention之间的关系是个问题：
1. 可以用一个FFN来将z映射到encoder_output_sequence的形状，之后继续用attention解码吗。这个可以现在rnn-vae中尝试。
2. 不管attention了，确定GPT或者BERT是怎么运用transformer做语言模型的单元的，印象里也是完全抛弃了attention模块。
3. 在transformer中本来前后attention模块直接用第一个模块输出和z向量之间做运算。

先把encoder换了试一下。

1. 模型前向传播，传入encoder的mask是怎么生成的？全是1，形状是什么？用处？我要mask什么东西？
2. 预测阶段怎么实现一步一步预测？
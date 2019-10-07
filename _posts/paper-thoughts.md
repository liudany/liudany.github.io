---
layout: post
title: 关于论文的乱七八糟想法
date: 2018-11-14 09:28:09
tags: [论文]
categories: [论文]
draft: true
---

# Auto-encoder

## 其他的生成模型

知乎刚点赞的

## transformer

transformer，self-attention的结构允许这么做吗

## zero-shot

[Meta-learning](http://ruder.io/10-exciting-ideas-of-2018-in-nlp/)

CPVR 2017 [Semantic Autoencoder for Zero-Shot learning](http://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1704.08345.pdf)，[知乎](https://zhuanlan.zhihu.com/p/27779811)

在中间层加入监督的限制。

## denoising

CS224n课中句子编码之后PCA投射到一个空间里（[论文](http://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf)），不管语序等问题，他们离的很近。我可以做一个然后表征他们离的更近了。

## 篇章生成 Paragraphs and Document Generation

ACL 2015[论文](http://aclweb.org/anthology/P15-1107) 

## CRF 

ACL 2017 [从里面看看会不会得到一些启发](http://aclweb.org/anthology/D17-1171)

## CNN-DCNN

加入denoise看看会不会更好。加CRF会不会好。2017。加入层级表示会不会好。加入variation会不会好。NIPS。算相似度的时候用CSLS其他论文中。

## CNN-RNN 非对称的autoencoder

CNN编码，RNN解码。RNN编码，CNN解码。合理，RNN得到一个带有时序信息的，CNN提高解码速度等。

一般的看图说话是CNN-LSTM，我们可以LSTM-CNN。

有人做过的话就用这个加上，hierarchy。加上document。（到底做没做过，可以通过DCNN那篇文章来看）

训练时候，预训练RNN和CNN，然后拼起来，看效果。

生成时候paragraph，SRNN？yuzeping的，先一个段向量，然后cnn解码出来

## VAE控制每个时刻的分布

篇章级别，有很多隐向量，用VAE方法控制每一个隐向量的分布。

## 长距离

是不是下一句

# Unsupervised System

Google在训练语料前加标注目标语种的token，用统一的一套参数来训练。

一种无监督的捕捉长距离的视频框架。[论文地址](https://arxiv.org/pdf/1701.01821.pdf)

## vae

两种语料的latent space对齐，即N(0, 1)空间的对齐，可以生成语料。

# Embedding Alignment

## CNN训练词向量

既然EILO可以用LSTM，那就可以考虑CNN训练。

## VAE

强制服从一个分布？对齐？

# Reinforcement Learning

可以解决不可微分的问题，比如一些attention。

# Back-transalation

也是一件generative的事情，和vae等思想或者generative能结合吗。

# sub-word的角度去解释一个词

做一个词典，解释含义

# VAE in machine translation

做一个多语种加谷歌的标签，到N(0,1)的映射

**在sentence level用denoise，来增强句子autoencoder的robust**

# Word Embedding

**中国CW分词用在sub-word上？用sub-word代替每一个偏旁，从词本身去得到。**

**在sub-word级别上去denoise？抛弃一些，调换一些？**

**用autoencoder生成词向量？反向？由词向量倒过来推词语？由autoencoder生成词向量有一个问题，和下面的LSTM有什么区别？反而是降级了，用LSTM做autoencoder？那用LSTM做autoencoder可以用在之前的任务？**

**hierarchy多层的denoise从subword到词到语言？**
NAACL最佳论文：带有序列信息训练词向量，之前的CBOW都是没有序列信息的。这篇文章用了LSTM的，而且窗口非常长。

用subword来增强词向量。基于字母的N-gram词典，

和普通BPE的区别是？

# 成语替换

让句子更有文采，成语替换。外国有没有类似的短语替换。
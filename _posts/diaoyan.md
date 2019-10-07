---
title: 生成调研
date: 2019-07-15 09:28:09
tags: [NLP]
categories: [NLP]
draft: true
---

# AAAI'18

## Long Text Generation via Adversarial Training with Leaked Information

LeakGAN：GAN+policy gradient可以用在离散的文本上，是一种RL的形式。在生成过程中让D泄漏信息给G指导

针对的问题：GAN RL中文本生成只有在结束了以后才有指导信号，长文本的话这会很没有效率。

提出的方法：每一步都提供一个f指导生成。![image-20190703142254756](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703142254756.png)

## A Deep Generative Framework for Paraphrase Generation
生成Paraphrase，VAE+LSTM，在encoder和decoder都依赖于源句。

![image-20190703143158257](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703143158257.png)

在encoding和decoding阶段都以original sentence的表示为条件。我寻思这个z意义不大吧？

死亡点名https://github.com/kefirski/pytorch RVAE。

## Controlling Global Statistics in Recurrent Neural Network Text Generation

这篇文章围绕additional statistical constraints，人为的给模型添加一些限制，而不是对参数作正则。

方法Dynamic KL Regularization，一边生成一遍算着分布，和你给出的限制分布作KL。

不是从参数上，而是从生成出来的东西现实的统计上。

## Event Representations for Automated Story Generation with Deep Neural Nets⚠️
为了生成coherent的story，把这个任务decompose为先生成event，再由event生成language。

认为词太底层，不能保证语句之间的连贯性。而句子太高层，太过于sparse，可能只出现一次。所以用中间的event级别，作representation。

![image-20190703151550569](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703151550569.png)

虚线部分还没实现，实线部分是框架。对于每个事件预测下一个事件，再把事件翻译成sentence。

## Tree-Structured Neural Machine for Linguistics-Aware Sentence Generation
普通的对话Generation不够充分的利用语言学规则，语法信息。

作者建立了语法树，用树状decoder来解码。

## Order-Planning Neural Text Generation From Structured Data
Table2text的生成任务，考虑table中不同field之间的先后顺序，来生成。

## Incorporating Discriminator in Sentence Generation: A Gibbs Sampling Method
![image-20190703154342569](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703154342569.png)

更新很多轮数，不相关的。

## Hierarchical Recurrent Attention Network for Response Generation Chen

![image-20190703155205251](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703155205251.png)

重点在层级attention，因为不同的utterance有不同的重要性。

# ACL'18

## GTR-LSTM: A Triple Encoder for Sentence Generation from RDF Data

从RDF Data（对象，属性名称，具体属性）中生成句子。

## Hierarchical Neural Story Generation⚠️

两个问题：长文本建模，连贯性。

第一个问题，用CNN解决了。第二个问题，用hierarchical解决了。

**去代码看看有没有分段！**

# EMNLP 18

## A Skeleton-Based Model for Promoting Coherence Among Sentences in Narrative Story Generation⚠️

提出基于句子skeleton的方法，提高coherence。

也分两步，先生成重要的phrase（skeleton，是一系列词语），再把skeleton变成下一个句子。

由两个模型组成，generative和skeleton-exraction，两部分之间用强化学习连接起来。

generative部分由两部分，input2skeleton，skeleton2sentence。

认为skeleton标注的数据集是没有的，所以用了一个生成器。

![image-20190703164004138](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703164004138.png)

## Diversity-Promoting GAN: A Cross-Entropy Based Generative Adversarial Network for Diversified Text Generation

用GAN控制生成的多样性和寓意连贯性。

# IJCAI'18

## Topic-to-Essay Generation with Neural Networks
![image-20190703172703441](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703172703441.png)

维护一个topic向量c，决定了后面的生成中更倾向于表达的东西。

## Toward Diverse Text Generation with Inverse Reinforcement Learning

又是一个强化学习。

# NAACL'18 19

## Discourse-Aware Neural Rewards for Coherent Text Generation
又是强化学习。

## Natural Language Generation by Hierarchical Decoding with Linguistic Patterns

![image-20190703173621328](/Users/danyliu/Library/Application Support/typora-user-images/image-20190703173621328.png)

按词性来分层生成，具体来讲是词性标注。

## Topic-Guided Variational Autoencoders for Text Generation ⚠️

混合高斯模型。

## Plan, Write, and Revise: an Interactive System for Open-Domain Story Generation

开源软件。



# ACL2019 Xu Sun

Story Ending Generation，是给定一个fine-grained sentiment intensity。两个问题，语料库，和显示控制情感。

由故事前面X，和给定的情感s，一起生成ending。

训练阶段s由一个sentiment analyzer来判断，文章里给了三种方法。

生成阶段，先把故事经过encoder，然后decoder部分由两个东西，一个是语义semantic generation，一个是情感sentiment generation，两个loss按照一定的比例加起来。

具体怎么用情感的，是Gaussian Kernel Layer先不用管。

# ACL2019 Martin

Event2sentence，普通方法只注重grammatically-correct，但是semantically-unrelated。

改进了event2sentence，用一个ensemble的模型。最后跟之前的event2event合作起来效果也不错。

用seq2seq经常会忽略输入encoder的event，退化成普通的LM。

用了4种模型的ensemble来实现这个事情，重点不在reinforcement。

# Reward-shaping

为了一个given goal，分析语料库，然后在pre-trained的LM上进行改进。

RL目的：控制一个特殊的目的（情感/结尾），并且coherence。

故事生成也可以看作一个Plan问题，只是用LM太过于简单，只是注重co-occurrence。

有一些communicative goal，比如主题，结尾，这些很适合用RL来做。

# 问题分析

## FB

没有彻底hierarchical，句子间没考虑到。

好处：是用了model fusion，去注意第一个模型没注意到的。

## Events

中间表示用的用的四元组，太死板，不够全面。

根据上一个event生成下一个event，缺一个主题来全面指导。

## Skeleton

在中间层的表示上，用的Compress句子压缩，质量不一定，还是比较sparse。

好处：用了RL这是好的地方，让skeleton extraction和生成一起进步。

## Plan-and-write

用Title生成Story-line，是一系列的词汇。一句一个词。

比Martin event的任务没进行故事全文的生成。

与Skeleton比，skeleton是动态的，这里动静都测试了。

## 可以的改动

1. Hierarchy的中间层表示到底怎么挑选，比较好。
2. Vae，篇章空间的探索上会更好。
3. 加个discriminator控制句子间的流畅，和主题的匹配。
4. 都基于rnn，可改为transformer快一些。
5. model fusion，丢失的东西？



# EMNLP'18 Automatic Poetry Generation with Mutual Reinforcement Learning Xiaoyuan

- They are all based on maximum likelihood estimation(MLE最大似然估计), which only learns **common patterns** of the corpus and results in loss-evaluation mismatch.
- Directly **model the criteria** and use them as **explicit rewards** to guide gradient update by reinforcement learning. 设计一些显示的reward。
- 称为一个criterion-driven training process，而不是MLE相似度驱动。
- **重点：这个方法是实现在一个用MLE来pre-trained的model之上的，也是一种fine-tune的方法。**
- **也是用的大写REINFORCE方法，（好像）是把刚才的预训练LM作为一个generator，用RL去修改它。**

# AAAI'18 Long Text Generation via Adversarial Training with Leaked Information

- 提到分层强化学习是用来解决reward太sparse的问题。
- RL的agent说的是啥？micro-policy？
- Recently, (Vezhnevets et al. 2017) proposed an end-to-end framework for hierarchical RL where the sub-tasks are not identified manually but implicitly learned by a MANAGER module which takes current state as input and output a goal embedding vector to guide the low-level WORKER module.
- 要明白我这个任务到底要不要显示的定义sub-tasks?
- GAN RL之间的关系，还要通过seqGAN来好好想想。
- SeqGAN中，G和D唯一的交互就是一个标量，但是G并不知道为什么。女朋友说不高兴，你并不知道为什么不高兴。这样改进的很慢，只是在猜，要花很长时间来更正。LeakGAN的想法就是抽出D用来打分的Feature给G看看，说不定会学得更快。
- SeqGAN中做蒙特卡洛，variance很大，无法采样足够多的，只能采一些。且时间花费很长。
- GAN在trainG的时候D是固定的，你给一个分数，它反向传播不会经过D，也就是并不知道到底哪里分数低，该往哪里移动，信息太少了。如果给一个feature vector就好很多。
- Worker不care整句话怎么样，只管manager给的。Manager最后的reward是整句话D给的分数。
- D是一个reward function。
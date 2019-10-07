# 结构

总的来看，是Intro，Method，Experiment(dataset, baseline, metric, result)，Conclusion。

对于这篇文章而言：

## Intro

## Method

先总体介绍，然后as illustrated in fig.1, our model contain two parts:1 。2介绍任务和符号

### Action predictor

这里embedding要介绍吗？

### Sentence Generator

## Experiment

### dataset

### Metirc

### baseline

### Result

Embedding图

结果对比图





character-based neural storytelling model



突出一个以人物为中心

## 一些词汇

personality 个性

actions performed by characters

a believable sequence of character actions

Character believability/ believable character

## Method

In this section, we will introduce our (模型) in details. Our model aims to (作用). We first (第一阶段), and then (第二阶段). Figure \ref demonstrates the schema of model.

我们显示的对人物进行建模

可以for example，就在method这里



提取数据的写在哪？



Character believability (Bates, 1994)





## 写法

如果你的模型复杂，就先preliminaries，然后method，最后related。

如果well-defined任务，简单模型，就先related，放大自己的highlight，然后接method。



## character embedding

1. 泛化能力，没遇到过也可以做出正确选择
2. 人物一致性，前后动作一致而不是仅仅依赖于共现关系



## 图表

好的人物一致性的故事

差的人物一致性的故事





Intro不要有逻辑gap

Result先来个大表，总分比一比分析分析。

然后各种ablation，各个模块的影响。

然后case study，好的case坏的case，坏的引出future work的。



Related最后写。





Intro

第一段，没讲任务的意义，或者现在有许多人在做，热点。印出来

including多写几个，among which ，娱乐价值，和一些要求long-range 等 narrative intelligence 关键词出现 coherence 既有娱乐价值，又有研究的挑战

提一下rule-based可解释性好，为什么用neural，他是个黑箱子，兼顾了可解释性和model句子的能力，data-driven。解释性，控制性。

rule-base缺点，需要标注，等等。

说我和现在的neural的区别。

character 和 action的关联，是一种可解释行

explanability，coherence，从大角度入手，controllable explainabilitiy，

对应，charactor action，每一步相关性，和character一致性，两种corherence

pay little attetion改成fail to，temple-based。

旗帜鲜明，从大角度，你是data-driven的，你是rule-based的，我要怎么做





review的时候，expalnability，rule-based缺点不要提了。

第三段讲我是怎么做的，用rule-based的哪部分，为什么这么做，neural-based

从nueral的角度 coherence是个challenge的问题，科技实行差。



任务，价值



四段的定位先明白，段的每个句子，先outline，总分的方法。

从大到小引入自己的问题。

逻辑关系。

第三段讲motivation从哪来。



看看c-vae



related work大家只关心你有没有cite它的文章，性冷淡风

但是intro里面review要旗帜鲜明🚩





comparable

Conduct

Outperforms






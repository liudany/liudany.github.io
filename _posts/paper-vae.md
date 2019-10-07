---
title: Go for INLG!
date: 2019-07-01 09:28:09
tags: [NLP]
categories: [NLP]
typora-root-url: ../../source
draft: true
---

# 1写作思路

- 在翻译的Transformer中是如何运用Condition信息的？类比到我们要做的东西中来。

- 比速度。Train/eval都比。
- 比较不同利用z的方法得到的结果，例如只cat，只用作hidden等。
- z用作lstm的hidden而不是cell，因为hidden和当前输入x可以相互作用，一起决定cell。
- 研究generation是一个广泛的工作，可以用在translation等等上面。

# 2写作思路

- 续写结尾上，给一个开头。
- 有了hierarchical，就可以做attention 了？
- 把长距离依赖问题分两级来解决，这样对每一级的长距离建模能力要求就会降低一些。

- 层级，时间地点人物？

- 想想人怎么写故事？？我先构思，然后想好每一段，然后
- 句子之间的attention，层级attention
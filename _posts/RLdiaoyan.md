## Toward Diverse Text Generation with Inverse Reinforcement Learning

解决两个问题：Reward太过sparse，模型collapse。

将文本生成认为是一个Inverse Reinforcement Learning的问题，认为training data是expert generated，应该有高的reward，学习这个reward function，模型分两步：

1. 学一个解释reward的函数。
2. 学一个generation policy，使得reward of trainning data得分高，生成的得分低。

用$\tau$来表示一个MDP马尔可夫决策过程，即一系列的state和action对应的序列，每个样本看作从这么一个$\tau$的分布中采出的样本。

Reward Approximator和Discriminator的区别在哪里？和seqGAN的区别在哪里？

## 要学习的

policy指的是生成还是什么

REINFORCE算法是什么


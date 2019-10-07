

# Day 67

用严老师的话就是Settle down，办了饭卡啥的还不知道啥时候发下来，先确定一下生活方式。

中午回去回来太折腾，而且浩然太吵，**戒掉午睡**。

**北大食堂，健身房。**

**英语怎么学。**可考虑中午时间，但是口语啥时间。

## 生活计划

7:00 起床洗漱

7:30 吃早饭

8:00-12:00 学习

12:00 出发吃午饭

13:00-18:00 学习

18:00 晚饭

18:00-20:00 学习

20:00 出发健身

21:00 结束健身 出发回北航

晚上雅思

## 学术计划

还要做2篇论文的准备吗？sure the more the better。

晚上的时间做做transformer-vae吧。

英语在回宿舍之后吧，睡前。

中午骑车找起头时候有了一个想法：(Conditional) Sentence-level Language Model，名字好像还蛮厉害的。

## Ideas

1. Paragraph生成，层级，这个肯定的。

2. Cross-lingual 词向量variational对齐方法。

3. 真正的Transformer VAE。
4. 无监督的摘要-扩写系统。

## 英语

剑桥4-10听力，阅读。八月之前重点把这两个项目搞好。

每天30分钟把流利说的课打了。

## 总结一下

1. 开始了T-VAE的Latex文章，骨架搞好了。
2. 几个提高效率小hint：No wechat No weibo No Zhihu No Airpods, Read Papers and Do Experiemnt



# Day 66

七点五十才出发，赶上早高峰了地铁不太舒服。今天是雨天。

今天把篇章生成文章再看一遍，主要做做Fairseq的Tranformer Encoder-Decoder吧。

**要连续思考，不要被微信打断。**

**摘下耳机听世界。**

## 框架选择

用Fairseq，还是用Pytorch自己写，还是用Keras或者Tensorflow，和学长同步工作？

确定好利弊：

- Fairseq：有现成的transformer模型，有语料库和预处理，有集成的evaluate方法，有beam-search等。但是不利于修改（框架上的修改？这句话），复杂，学起来困难。
- Pytorch：简单清晰，缺点是后面加东西不方便。
- Keras/Tensorflow：是必须要学的，有一定学习成本。但是可以和学长沟通。

## 要解决的问题

1. Fairseq框架下改出来VAE。

   - 在encoder和decoder之间加入分布操作。

     - Batch操作批量的产生z需不需要更改细节。

       在encoder最后，h->z。**在deocder开始，z->h为了维度。**

     - dict存放out的形式，在encoder还是decoder改比较方便。

       z放在encoder结尾，在decoder开始把z变成h。

   - 输入和输出是一致的，重构任务。

     - 寻找Task怎么改，输入输出怎么改。

   - Loss函数要改。

   - 显示一些训练过程中的参数。

2. 在翻译用的Transformer模型中是如何利用条件信息的。

   是用Attention捕获条件的，同样在基础RNN中也可以完全基于attention而摒弃了显示的一个条件。

3. **跟学长的谈话好好准备outline，这个课题的可行性等等**

## 要问学长什么问题

1. 课题上，这个题目行不行得通？前人做过什么工作
2. 框架上，选哪种框架？有没有必要统一起来
3. 读论文和做实验的平衡，读论文但是很多是VI另外的分支，和我想做的不太一样。
4. 总体计划安排，怎么做一篇论文
5. 我很没信心，不踏实，不知道这个想法是不是值得做

## 存在的问题

1. **为什么是logvar，为什么torch.exp(0.5logvar)得到方差。**

   顾名思义log variance，因为神经网络得出来的可能是负的，而方差是正的，所以用log把值域转到实数上来；化简为2log standard deviation，所以除以二作指数刚好是方差。

2. 又动摇了，到底用哪种框架，不能确定这个浪费了我很多的时间。
3. 改task，criterion要跳很多文件看很多代码，头疼，这是目前最烦人的问题。

# Day 65

## 今天要解决的问题

1. 框架选择
2. 课题可行性
3. 和学长聊天

## 聊完了！

真的没有那么简单啊。

## 研究方法上

一个问题 要有价值，看看别人的工作。

切入点，怎么讲故事。

不用学了，与tensorflow有关的baseline他直接跑给我。

先调研，综述，要相当充分才可以。Text Generation。

做科研，是你想解决一个问题，然后才有的其他。

## 论文安排

可以两片，equally。一篇我只做实验，其他的他来搞。一篇我做实验写draft，他帮我润色。

一年一新，2018年的就是玩剩下的了。

一定要调研好！别人做了什么，没做什么，先确定这个课题有没有被人做过。

## 研究领域

Low resource: data augmentation/selection

Cross-lingual

## 安排

先把调研做好，每篇文章用了什么方法解决什么问题

Low resource综述

## 突然

想学会GAN+Reinforcement，目前GAN的策略都是policy gredient。

在模型创新上下点功夫？目前还没有VAE+reinforcement，用award控制这个隐变量？

## 聊了聊

1. LM只是代表一个incremental的解码方法，你调用了好的API，结果就变好，不要太拿这个当回事儿。所以Trasformer这个不算大创新，只是换了种LM模型。
2. 投稿要中，不仅要效果提升了多少，还要让人有眼前一亮，学到新东西的感觉。
3. RL是离散的？这个需要学习。再看看她的文章。
4. 强加VAE你想干什么，你要看到它有什么问题，然后想办法用某个工具解决它。不是你会VAE就往上加，倒过来做不可取。
5. 中间的表示上，有global的也有private的，共同指导着下一步的生成。
6. 你来学习抱着积极一点的心态，有进步要开心点好吗。
7. 说话上，注意一点。你直接说他们用了不同的，我也用个不同的，那人家当然以为你是为了不同而不同。说明白他们有什么问题，RL有什么问题，keyword有什么问题，你用什么方法来解决，说话有因有果。

## 与昨天相比

我发现变了很多，我现在脑子里想的如何解决故事生成中遇到的一些问题，而不是如何强行把一个东西用在任务中（且前提并不知道它好不好用），这也算是一种进步吧，开始总结不足之处，寻找改进之法。

且知道了怎么发论文，不是效果更好就可以，要让人眼前一亮，感觉学到点新东西。

每次聊天以前想好了话要怎么讲比较得体，让人能听懂你的来龙去脉。

## 问题

生成一些中间层的表示，怎么训练？

Events用的自己的提取算法，skeleton有自己的提取，keywords就是词向量。

没得对比，就有variational？在动态中寻找到最好的方法？

# Day 64

上午去拿通行证，被告知下午来。然后上午疯狂找租房信息，租卡信息。

下午去拿了通行证，发现自己还是蛮帅嘛哈哈哈。花了600多块钱租了一个太阳卡，押一付一，算是有办法吃饭了。去健身房办了健身卡，是学生身份很便宜。这样一下午基本过去了。

晚上跟起头去游泳，说说话，心里舒服了很多，挺压抑的这两天，经历了一些“被否定”还是挺不爽的，不过忠言逆耳嘛，要进步得忍受这些东西。

# Day 63

原来周五上午有组会。

不要囿于，看新坑。你对文章生成，生成模型这部分真的很懂吗？好像也没有。所以努力开辟新领域，跟着老师和学长就去学一些他们擅长的东西，比如说low-resource和cross-lingual！两个方面同时进行吧。

想搞一个中文故事语料库。



data selection做个工作！

## Story

构思人物，人物性格，做事。

人物之间的关系。

Character representations

## 任务

1. 读EMNLP学长审的这篇文章。
2. Gibbs 采样。
3. 看RL和对抗在文本生成中的基本点。
4. lili的使用RL的方法，读一读。
5. 看明白数据集什么样的，能不能用决策的过程（离散化的）在latent state flow里面。
6. YANG LIU文章。

## RuiYan

一次做一件事情。

## 知识栈

RL！

## 不可微

到底什么是不可微

# Day 62

看完了李宏毅关于GAN和RL在序列生成的视频。

大体还是一个Conditional GAN的框架，普通GAN因为sample无法反向传播，这里用RL的policy gradient解决这个问题，给每一个行为一个award去加权梯度。

也知道了CycleGAN其实早就做了自己想做的事。

## 今天搞明白两个问题

Sample不可微分，那arg操作可以微分吗？那平常的Maxlikelihood 是怎么优化的？他也有采样的过程啊。

BLEU不可微分什么意思。

> ```
> D:因为离散的序列在梯度微调时没有意义。
> 
> G:即使用的是word2vec之类连续的，微调之后可能得到一个什么都不代表的向量。
> 
> I:在文本生成里面，尤其是用了word2vec的。我这边提一个问题，我也不知道业界有没有方案。就是生成的向量是在空间里的，基本不可能对应到有意义的点（word），那么只能取最近的，那么如果这个向量做了优化，对GAN来说是非常敏感的，也许判别器就更难判断了，但是对词典里的词，是不敏感的，也许距离这个生成的向量的距离的排序没有改变。
> ```

那么平常的生成任务怎么就有意义？

> ```
> policy gradient和gumble softmax
> ```



> ```
> A:感觉CNN做判别器比较多
> ```

判别器选择上。

## 以后安排

每天读论文，想Idea，做实验（没敲定主意之前，写代码）。

下周去开会了，transformer-vae是不是安排一下。

## 今天

写一个sample然后反向传播的试试

# Day 61

## 工作

明白GAN和RL的意义，用法，简单代码实现一下。

安排以后

# Day 60

看CVAE-D流程。

看Skeleton流程。

看Topic-guide流程。

看SLDS流程。

## 先找清楚出发点

是想往下迈一步，做更精确的控制。

还是要做fine-grained的问题，比如thematic-consistent，diversity等等。

还是有其他的出发点。

引入额外的信息。



然后想架构，一定要带着想法，下次去跟学长聊。

今晚就搞定这个问题。

# Day 59

## 日期安排

一周写论文，一周改论文，最后留出两周。所以8/17之前做完实验。

7/22回来，那就是7/22-8/17，27天的时间做这个实验，四个周。



## Skeleton

它目标是**Promote Coherence**，提高句子之间的连贯性。

先生成句子最重要的phrase，即skeleton，这个东西是通过RL学的。

核心思想是使用全部词汇会使得句子表示太过sparse。

### Cons

没有注意thematic的要求，虽然有input但是用的LSTM结构的seq2seq，主题信息会慢慢丢失。

即，生成过程中缺乏global信息的指导。

**虽然用了RL，但是用RL训练的skeleton extraction模块，无关故事的Plan。**

**规划下一个skeleton的模块是language model的原理。**



## Plan and Write

给定标题/主题，分Dynamic和static两种方式。

Dynamic是keyword->sentence->keyword->sentence，有flexibility。

Static是先生成{keyword}，之后再把topic和keywords压缩到一个vector，指导着一次性生成{sentences}，有coherence。**并没有用每一个keyword去指导每一个句子生成。**

### Cons

Static中不能确保开始的keyword会被记住，thematic被逐渐遗忘是肯定的。

**看看facebook的论文怎么说的遗忘这件事。**

**做Plan的时候也是基于language model或者MLP。**



## Event Representation

说word级别的生成，太低级，不会关注到sentence之间的coherence。

而sentence级别的生成，因为sentence representation太过于sparse，难道model这么sparse空间内的关系。

**目标：减少句子表示的sparsity而且尽可能保留语句的信息。**

用event2event来生成event序列，再用event2sentence恢复出可读的句子。

Event是主谓宾和其他的四元组，用斯坦福的dependency parser解析出来的。

### Cons

没有注意thematic，只是一系列的event往下走。

**做plan的时候用的language model，其实考虑共现。**

## 想做的

**之前所有的工作都是用LM来预测下一个句子，还是考虑的共现概率，实际上可以认为是个规划问题。Martin说的这是一个communicative goal，例如关于某特定领域，包含某主题，或者以某种方式结束。**

**这非常适合用RL来做story plot的规划！蒙特卡洛搜索完毕看看是不是满足某一个要求。**

**主要是设计reward。**

加入sentiment引导。

diversity，thematic。

生成句子，然后根据我们的情感给他一个情感变化！先生成句子，然后rewrite！

## 突然

读的好开心啊感觉～舒服～



## 整理整理思路

你的目标是什么？

普通的LM方式生成下一个事件，考虑的更多的还是common pattern，用policy gradient可以更多的关注我们需要的特性，人定的目标。



1. 我们需要什么特性。martin是要最后出现一个什么动词。我们是sentiment flow。
2. 对什么用RL做预测。martin对event，我们应该也是对event/keyword，做预测。

3. martin先训练了一个event2event的LM，我们训练一个keyword->keyword的。plan-write。

4. sentiment以什么样的形式出现？训练时是提取的，生成时是人为定下来的。

   看看古诗生成的论文。要写故事，那是给定一个sentiment，还是自己生成？

5. 还想关注一个thematic。

   这应该是reward里面关注的东西？



衡量sentiment flow的标准也好办，用pre-train的模型去看生成flow和我给定的是不是一样。



# Day 46

回来啦，先午睡一下。

# Day 44

读论文发现了古诗生成用的**Semi-VAE**是以前没学过的半监督方法，不是sentiVAE！什么眼神。

找到了bjlkeng的博客！非常棒，有时间学习一下关于VAE的基础文章。

# Day 40

新的ACL论文出来了，找到3篇相关的，学习一下。

我们的目标函数可以有两部分：是否是连贯的句子，情感极性对不对。

# Day 38

重要的是你学会了这个科研的流程，该怎么进展。

论文重要的是你解决事情的角度和方法，角度是问题的看法和切入点，具体用RNN/Transformer这些不是角度；方法也不能是堆积，要有好的insight。

生活重心不要偏移，有大局观，什么才是最重要的。

分3大步，确定好每一步的创新点和做法。

## Sentiment抽取

| 论文                                                         | 抽取方法                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Sentiment-Controllable Chinese Poetry Generation             | 全篇有一个总体极性，每个句子有从negative到postive的五种极性，用了一个半监督的semi-vae。 |
| Learning to Control the Fine-grained Sentiment for Story Ending Generation | SentiAnalyzer给ending句子一个fine-grained的从0到1的**sentiment intensity**，用了三种判断极性的方法结合起来。用了Gaussian Kernel Layer判断生成词的极性要与总的senti接近。 |

## 中间表示

| 论文                                                         | 表示方法                                                     | 表示之间生成                                           | 表示2句子                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------ | -------------------------- |
| Plan-And-Write: Towards Better Automatic Storytelling        | 用的keyword，每句提取一个词，用RAKE，importance of word来选最重要的那个。 | 都是用LM的方法，分动态和静态。                         | 语言模型，利用了题目信息。 |
| Event Representations for Automated Story Generation with Deep Neural Nets | 四元组event，用主谓宾和其他，用Stanford的parser工具生成的。  | RNN的seq2seq，四个时间步输入四元组，预测下一个四元组。 | LSTM                       |
| A Skeleton-Based Model for Promoting Coherence Among Sentences in Narrative Story Generation | 用Skeleton，实际是句子压缩的任务，压缩为一系列词语。         | 没有表示之间生成。                                     | Seq2seq                    |
| Story Generation in a Switching Dynamical System             |                                                              |                                                        |                            |
| Controllable Neural Story Plot Generation via Reward Shaping |                                                              |                                                        |                            |

Pytorch TensorFlow可以混用的。

# Day 36

连续的坏处：太过于sparse，在空间内分布离散，不好decode

离散的坏处：信息不够完善

用VAE的好处：保证了空间内的连续分布意义，每个点都可以decode出来。且不用离散，不用丢失信息。

被否定了……

套一个东西过来解决这个问题，要跟当前任务结合一下。情感？或者什么

模型改进可能不要很大，但是要有一个出发点，跟任务结合的

## Neural News Recommendation with Long- and Short-term User Representations

用denoising autoencoder和GRU去得到user embedding。



决定从人物的角度。

人来做动作是有一定随机性的，有一个动作空间action space，应该是采样比较合理的，对一个situation怎么act

>  南派三叔在谈到自己的创作时，曾经说只要把自己的人物放在特定的场景中，他们就会自动按照各自性格做该做的事，说他们想要说的话。

人物向量，总的场景向量，LSTM？cell state？

Situation，Character，Action这是最基本的，

设计一个流程。

# Day 35

今天把这几篇论文读完，总结出一个适用于DL的框架。

## 人物肖像

### 07'ACL PERSONAGE: Personality Generation for Dialogue

Big Five人格。

### 13'ACL Learning Latent Personas of Film Characters

### 16'ACL A Persona-Based Neural Conversation Model 

好！真好！他们要捕捉说话的特点等，我们要捕捉做事情的方法，对action的决策。

### 18'SIGDIAL Controlling Personality-Based Stylistic Variation with Neural Natural Language Generators

目的是根据同一个语义向量生成风格不同的回答，用了两种方法，一个是加人物的标志位，另一个是做一个context vector指导后面的生成。

### 18'EMNLP Learning Personas from Dialogue with Attentive Memory Networks

对话，用分类任务去台词中学persona embedding，trop是个啥。



之前有人做过，反而是一个支撑，在神经网络时代没有人做过。



一句话读不懂的时候怎么办？



# Day 34

继续读论文。

# Day 30, 29

### 16'ACL A Persona-Based Neural Conversation Model

- 在user embedding空间相似的人，可以互相infer他们的act，即使在训练集中从未出现过。
- user embedding是和word embedding等其他参数一起在训练阶段训练得到的。

### 13'ACL Learning Latent Personas of Film Characters

- 提取出人物采取的行动，人物被采取的行动，被人对他的描述，来构建。

## 存在的问题

- 做单人物还是多人物？

### 训练阶段

- 多人物情况下，可以提取出主语和宾语，做一个interaction向量，指导verb生成。

### 生成阶段

- 每个句子如何决定单人物还是多人物，好像可以由当前的situation embedding来决定这一句有几个人出场？有的话都有谁呢，比如我有五个人物去选其中的几个。
- 谁是主角的问题，简单情况可以只有一个主角的故事。

## 待解决

### 语料库的选择

- Martin用的电影plot，刚好是Learning Personas那个。
- Skeleton JingjingXu用的visual story的文字部分。
- Plan-and-write用的ROCStories。

### Character embedding的生成上

- 用离散的还是连续的？离散的比如五大人格，连续的直接encode
- 方法1: 随着LM的训练，一起训练出来。为每个人物随机初始化一个embedding，然后跟着LM一起训练出来，这样就不需要利用一些先验信息了。
- 方法2: 把相关信息encode为一个固定的东西，可以作为固定的，也可以作为embedding的初始化，再按照法1的方法继续训练下去，修正这个初始化的内容。这种方法下需要

### Story的框架上

- Character embedding的生成要在训练/生成之前，之后再借助他来进行LM的训练。（？）

- 分两阶段，人物-动作-句子来生成，还是一阶段直接用人物向量辅助词汇预测。
- 训练阶段，没有主语的句子
- 生成阶段，怎么生成人物，还是用之前存在的人物

## CMU Movie语料库

分为一个Dataset，有wiki扒下来的plot summary，和Freebase扒下来的表格数据；和其经过Standford NLP处理之后的文本。

### Raw

- Plot summary里面是电影ID号对应着summary，单纯无其他的。
- Character metadata里面是ID号，姓名，gender，生日，种族（？），演员（？）。

### Preprocessed

- 是XML格式的。
- NER是name entity识别，看看哪些是实体，公司名地名人名数字。
- POS是词性标注，一个词是什么性质的词汇，动词名词形容词等等。
- Lemma表示词汇的原型，去掉第三人称复数等等。
- CharacterBegin/Off表示从第几个字母到第几个字母是这个词。



要写代码了兴奋吗兄弟？？！！！！

# Day 27

把官方LM看完了。

# Day 26, 25, 18, 16, 15

## LM or Seq2seq

- 从网络展开后的角度看，都是很多个RNN单元的连接。
- 但是seq2seq显式的分为两部分网络，encoder和decoder，各自针对不同的领域。
- seq2seq可以完成**两个变长序列之间的映射**。
- 从上句预测下句的角度讲，seq2seq完成N对M的映射。
- 或许seq2seq可以让一个网络更专注于编码，另一个更专注于解码？

- 从学长的实验结果看，LM好像取得了更好的成绩。

## Pre-process

先tokenize，遍历训练集语料确定词表大小，不认识的词全部换成<unk>。

有必要lemma之类的？提取词语的原型，BPE可以解决这个问题。

划分train/valid/test，38308/4000/4000。

## Transformer

把最新的transformer model也瞅瞅。

## 读取人物信息

其实这个人物只存在于这个句子内，怎么才能让他更有利于句子的生成呢。

鉴于当前BPTT的形式，怎么确定一个故事的起止。句尾有<eos>。

第一种方法，先简单的**学习**一个人物信息，然后帮助预测。

第二种方法，分两个阶段，人物精确预测动作，然后整体一起预测句子，分两个模块训练。



读取xml文件，或者自己抽取。先试试读文件。

根据sentence id分开的，每个句子中会有多个人物id，多个动词。



Martain把word stem了，这样会不会提高BLEU。

## Batch

Batch的存在让提取人物变得复杂，如果有batch维度，那也不能用<eos>记录首尾的方法来训练了，比如第二个batch维度的数据并不知道是第几个故事。

必须要让Batch维度变成1吗。

记录一个同ids同形的记录在训练集中第几行的，可以记录是哪个story。

## 划分story和sentence

只划分story，取一个主要人物，多个主要人物，concat到hidden上去辅助预测，这样就不用管句子不句子，非常粗的一种方法。

划分sentence，每个句子有更精准的人物，和动作等。

划分出来干什么？方便与划分好的句子对应上，知道这个句子中的主语是什么，每种成分是什么。想清楚。

所以我只想让训练时候，输入的每个句子和corenlp处理过的对上。



## Lili提供思路

不一定要在训练时候对上，可以直接处理数据集，把模型的难度转移到数据集上。

This is title <EOT> Person Action <EOP> Sentence1 </s> Person Action <EOP> Sentence2 

这样可以直接输入LM训练，就简简单单的语言模型，可以说利用了这个信息。

额外训练一个Person Action的模型，由person和当前预测action。



1. 分句加</s>标志。

2. 加故事结束符<EOS>。

3. This is title <EOT> Person Action <EOP> Sentence1 </s> Person Action <EOP> Sentence2<EOS>

4. 或 This is title <EOT> Sentence1 </s> Sentence2<EOS>，同时并行的有

   ​	This is title <EOT>Person Action <EOP> Person Action <EOP>。

5. 有多个主语，<NER>是PERSON可以识别，多个动词<POS>是VB可以识别。

从Lili这个代码，你知道了论文怎么说是一回事，实际怎么实现是另外一回事。

和学长只需要谈高大上怎么说，不需要谈你怎么dirty的实现它。



你要做的是训练出一个，训练结果很完美的模型。

真正生成模型，生成出了什么东西，那个你自己说了算的。

不管第一层模型怎么判断，第二层模型我会用teacher forcing也就是正确的动词去预测该句子。



确定句子长度是否匹配。

读取哪些词？



我必须要做出来。

先跑第一版本，有效果，开始撸模型的部分。

介绍模型，公式，框图之类的。



做一个故事的时候，人物不需要名字，只要知道他是第几句话对应的那个character embedding，就可以输入这句话。

输入这个句子中存在的所有动词（若有人物，人物相关的所有词），和人物。放到前面。

人物，由它相关的所有词，决定。

也可认为句子里所有的动词都给出现过名字的人。





写完baseline，写完setting模版，放个表格上去

然后引用文献库管理好。

Martin语料库

Seq2seq找代码。

有些话不需要说，你自己默默做，最后说结果。你真的不想投了就不投了，重在过程吧。peace。



标点符号让ppl波动十几。

### 代码有几件事

1. 自己prune，截断一下语料库，让lili模型跑。（需要2，网速要求不高）
2. 把martin跑起来，并看看他的语料库能不能用在1任务中（找到prune后的语料）。（需要好的网速）
3. 找seq2seq的pytorch代码修改，要在一个好的基础上进行。（网速要求不高）



只有为了一个好结果，要1？自己编不就行了。2是为了1？maybe







题目：



A Character-Centric Neural Model for Story Generation

Towards Better (Automated) Storytelling: From the Perspective of Character

Incorporating Character Guidance in Automated Story Generation

Exploring Automated Storytelling From the Perspective of Character
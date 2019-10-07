记录coding过程。

# Language Model

目前想找一个最靠谱的，觉得会有很多trick在里面？

## 工程问题

- 在服务器Deploy到本地的时候，Mapping表单里Deployment path必须要填，即使是个/。
- 安装完anaconda之后，python还没生效为conda中的，要source ~/.bashrc。
- Terminal要ssh连接到远程……别傻乎乎的
- 环境搞得有点多，弄清楚了自己。

## LM trick

1. 每个句子的结尾，和下个句子的开头，这个隐状态要继续传递吗？

   每个文件的ids序列是连续的，不区分不同句子的。但是在batchify的过程中，按照batch_size直接切分，每个batch之间是独立independent的，即一个连续句子之间的相关性也会被切割，不同句子尾首相连，反而会连续处理。

   原因是为了more efficient。

2. 各层的初始化方法要特殊调整吗？

   Embedding层用uniform_，decoder到词表的映射bias调0，weight和encoder一样。

   同时还有tie_weights的方法。

   对于rnn的初始状态，有init_hidden函数，都是全0初始化。

3. Dropout要用几次？

   两次。对于词的embedding首先drop一次，经过rnn后得到输出，再drop一次。

4. 梯度裁剪：

   在每个bptt步结束后，进行`torch.nn.utils.clip_grad_norm_(model.parameters(), args.clip)`对这些参数的gradient位进行裁剪，不要太大。

## LoadData

data.py下有两个类，Dictionary和Corpus。构建语料库的时候用的data.Corpus(path)这种方法。Corpus中会使用Dictionary方法。

### Dictionary

初始化构建word2idx和idx2word，包含函数add_word添加新词，魔方方法len可以返回长度。

word2idx用的{}词典，是以word为索引的，所以不能直接list，要用词典。添加新词的时候，`word2idx[word] = len(idx2word)-1`，注意这里len是从1开始的，序号要减一。

idx2word用的[]list，给一个idx可以直接认为是下标，list是有序的，取出对应的word就行。在添加新词的时候，直接`idx2word.append(word)`。

有点极简主义的感觉！

### Corpus

初始化时构建dictionary，并**tokenize**提供的path下的三个文件train/valid/test。下面说的是tokenize的具体实现。

第一步是Add words to Dict：

打开文件，按照行来split并加eos结尾，对这个words的list中的每个词进行add_word。注意这里没进行特殊的操作，所有词都加，在add_word函数内部已经加过判别语句了。

第二部words变为idx序列ids：

先开一个长度为tokens(所有词汇总数)的LongTensor名为ids，然后还是按行操作，对每个词在ids的对应位置添加word2idx[word]，这样就得到了一个一维的idx序列，ids。

### Batchify

将之前的一维ids，裁减掉trim off到batch_size的整数倍，然后加上batch维度。

最终产生train/val/test三个data变量，每个都是(seq_len, bsz)二维的。

## BuildModel

记录vocab大小，传入RNNModel的参数中，部分参数意义：

| 参数       | 意义                                             |
| ---------- | ------------------------------------------------ |
| tied       | 即最后映射回词表的decoder层的参数与embedding相同 |
| emsize/nip | 词向量嵌入的维度                                 |
| hid        | RNN网络的维度                                    |

两次drop，embedding之后一次，rnn的输出再一次。

建立criterion，用的Crossentropy。

**注意这里没有做optimizer，后面自定义的。**

## Training Code

### repackage_hidden

将hidden从之前的计算图中解放出来，只保留其数值。

### get_batch BPTT(滑窗)

之前将一维的ids变成了(seq_lem, bsz)，**这里对seq_len再次切分，并右移一位产生target，**得到的输入data是二维的，但是target这里flatten为一维，是后面criterion求loss要求。

注意尾部的处理，`seq_len=min(bptt, len(source)-1-i)`，若最后不足bptt就用最后那点儿。

### train

- 首先打开dropout用model.train()。
- 初始化total_loss，起始时间，词表大小ntoken，初始化RNN的hidden状态。
- 在训练集上迭代bptt的时候，i记录当前bptt位置，batch记录当前是第几个窗口。
- 先把hidden从之前解放，然后zero_grad model criterion backward常规操作，这里criterion把decoder最后输出的三维flatten到二维，最后一个维度为vocab上分布。
- 对所有参数进行梯度裁剪。
- 参数更新的方法用手动的`p.data.add_(-lr, p.grad.data)`方法，即SGD。

- total_loss累加当前bptt的loss，每log_interval个batch来显示一次这200个bptt batch中的平均loss，不至于太密集。时间除以log_interval得到每个batch大概用多少毫秒。最后重置total_loss和start_time。

### eval

- 使用model.eval关闭dropout功能。
- 同样初始化total_loss，ntokens词表大小和hidden初始化。
- 打开no_grad功能，防止计算进入计算图内。
- 这里不用在batch上进行for循环了，直接全部进行bptt循环。准确的说是不用记录batch信息了，只记录bptt整数倍，batch是其目前进行到第几个窗口的意思。

### loop over epochs

最开始给一个初始的lr，和best_val_loss。整个框架用try和except keyboardinterrupt进行。

对于每个epoch，记录当前时间后，进行`train() -> evaluate(val_data)`，注意一个train()语句就是一个epoch，对于整个train_dataset按照bptt窗口大小过了一遍。

如果当前的val_loss是最佳的，就torch.save保存模型。

而如果当前val_loss经过一个epoch训练后并没有变好，就把lr除以4。

### final stage

最后测试test上的表现，还可以保存为通用格式ONNX。



## 心情

别的不知道，自己是好兴奋哟。Coding是让我兴奋的事情。

且不知疲倦，可以坚持下去，写这东西我真开心。
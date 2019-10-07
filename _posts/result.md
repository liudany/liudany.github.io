# 结果记录

## 原参数，LM

| End of training | Method          | test ppl          |
| --------------- | --------------- | ----------------- |
|                 | Plan-write      | test ppl   60.32  |
|                 | character-based | test ppl   54.53  |
|                 | Language Model  | test ppl   115.06 |
|                 | Event           | test ppl   53.96  |

sjtu4

Train1 Lili自己的corpus，与本次试验无关

Train2 我们的corups，title action sentenes的形式。

Train3 Lili提供的纯语言模型的训练，在我们的数据集上。把这个当作基线？





句子做split和prune，每个动词放在句子前面。

截断句子长度。

看代码怎么处理storyline部分的。

研究vocab。

句子截短，篇章截短。



想一个demo给shelly。



But,so 这种连词全都换成句号。

介词短语无视之。

可以找martin处理过后的，放到lili那个里面试。



| model          | b-1  | b-2  | b-3  | b-4  |      |
| -------------- | ---- | ---- | ---- | ---- | ---- |
| lm             |      |      |      |      |      |
| Seq2seq        |      |      |      |      |      |
| Hierarchy      |      |      |      |      |      |
| Plan-and-write |      |      |      |      |      |
| Proposed       |      |      |      |      |      |


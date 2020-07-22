## ACL 2016

最早，提出了数据集SIND，是连续的图片，配上描述，和故事。前者是互相孤立的，后者之间互相依存。

提出了**baseline**和**自动指标**。

讲了caption/description和narrative的区别，分三个级别，完全独立，完全故事，和中间的过度。

### baseline

基本模型之上做了一些heuristics的小改动。

1. 图片->fc7 vecotrs->RNN->image seq的表征->decoder->beam search->word by word
2. beam size 10 -> high level -> This is a picture of ...
3. beam size 1 <-> greedy decode -> story 变好 caption 变差 -> story重复 -> 同一个词不可以出现两次

## Multimodal Storytelling via Generative Adversarial Imitation Learning

搜索有关的，reinforcement learning

## Image Description using Visual Dependency Representations

先前的图片描述是unstructured的，没有表出object之间的关系。现在想搞出region/object之间的关系。

即infer出action，不同的object之间的action，而不是BOW一样单独列出。

编码了不同区域之间的geometric relations，几何关系，或者说八种dependencies。

文中用的是template-based方法生成的，基于cv的object detection技术。

从geometric关系推广到所有的动作关系。

只是单一图片的，我们可以建模一系列图片之中的region变化关系等等。



## Movie Plot Analysis via Turning Point Identificatio

剧情中的转折点，可以将长的叙事分割为一些小段落，利于处理长的文本。
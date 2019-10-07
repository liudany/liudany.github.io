# Seq2Seq

## Encoder

基础流程：input->embedding->GRU->outputs, hidden

### 双向结果的处理

## Decoder

需要的东西：encoder outputs, last hidden,

基础流程：input(指不定是上一步生成的还是ground truth)->embedding->**dropout**->embedded

另起：last hidden of decoder & encoder_outputs -> attention weights-> bmm encoder outputs->context

合起来：concat(embedded, context)->GRU(with last hidden)->output, hidden

注意结果：**concat(output, context)->Linear(2hidden, output size)到词表上**->log softmax->output

## Seq2Seq

取一个batch的src->encoder->encoder-outputs和hidden->按步decoder
以概率的形式来决定这一步是要teacher forcing还是要ground truth训练。

不是可不可以变长训练的问题，是batch training必须要padding到同一长度的问题。
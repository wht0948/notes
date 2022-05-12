## AdaPrompt: Adaptive Model Training for Prompt-based NLP
https://export.arxiv.org/pdf/2202.04824.pdf

![image](https://user-images.githubusercontent.com/32132519/168015171-e55ee540-d085-4956-bd63-28a2f782eea4.png)

背景：1、减少下游数据和预训练数据间的gap；2、增加label单词候选

1：首先对下游要预测的文本构造prompt并进行预测，对预测结果在通用语料库中进行检索(TF-IDF等)，找到相似的语料构造一个新的与下游任务相关语料库进行继续预训练(这个过程可能会重复好几次？)

2：首先人工选择几个label单词，如good、bad等，之后通过模型预测出的word(附带原始文本？)和已有的label(附带同样的文本？)进行比对(NLI系统)，如果很接近则将其加入到label单词中。

### 论文题目想不到了

背景：finetune一般有两种方式，第一种是训练全部参数，第二种是只训练分类层，特征提取层不训练。第一种方法上线更高，但容易过拟合，第二种方法上线比较低，但是效果一般不太好。

方法：结合两种方式，先训练分类层，训练完后再训练全部参数

### rdrop
训练时前向传播两次，因为dropout的原因会存在两次传播分类前的embedding不一致，对这两个embedding做kl散度来作为一个多任务的loss（感觉提升可能是类似模型融合带来的）


### batchformer
在batch维度引入多头注意力，增加batch中不同样本间的联系，使得每个样本的loss可以反向传播至其他样本上，类似一种数据增加。具体做法比较多，最简单的是对每一个样本最后的embedding做attention，即B×D的数据看做1×L×D，因为多头注意力不加postion id，所以顺序无关，过之前和过之后都经过同样的分类器去计算loss（视不同的任务也可以使用不一样的分类器）
https://arxiv.org/pdf/2203.01522.pdf   https://mp.weixin.qq.com/s/1AVW4KFoV1Rboxl1-B58Fw

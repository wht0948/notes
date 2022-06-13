各种bert
**roberta**  更大batch，更多数据，使用动态mask
**bart** encoder+decode，在encoder上mask，decoder上解码
**T5** 两次预训练，第一次MLM，第二次加上具体任务，prompt类型的预训练，核心是将所有任务换成seq2seq
**albert**  缩小词表 embedding， 通过一个矩阵增维和后续hidden size一致，跨参数共享，使用SOP（预测两句话有没有被交互顺序）  模型变小，预测时间不变，并且需要更深才需要和bert效果相同
**ELECTRA**  使用MLM生成的token判断这个token是不是和之前的不一样  包括生成器和判别起，生成器的目标是最大化判别器的loss，通过policy gradient
**transformer-xl**  使用递归机制，将文本切断，前面一段的文本会冻结梯度参与这一段的计算，即Q(n*d)✖️K(2n*d)T✖️V(2n*d)=n*2n  ✖️ 2n*d = n*d，同时将绝对位置改为相对位置。
**xlnet**  集合AR(代表GPT)和AE(代表BERT)两种训练，将句子重排，预测最后1/4的token，设计attention mask的修改，内容信息和位置信息的拆分等等。
**deberta** 有13层， 前11层只用相对位置编码，后面两层加上绝对位置，下游应用只用12层
**roformer**  用乘积position，使用绝对位置实现相对位置，即(Rmq)T  * Rnk =  qT R(n-m) k，不需要训练参数 https://spaces.ac.cn/archives/8265

长文本/线性attention
**Linear transformer**  去掉softmax，改用核函数，做到先计算K*V，最后成Q
**reformer**  通过LSH计算（近似地）快速地找到最大的若干个Attention值，只计算这些
**performer**  通过随机投影将attention线性化
**linformer** 对KV乘一个矩阵对长度降维  Q(n*d)K(n*d)V(n*d) -> Q(n*d)K(m*d)V(m*d)
**longformer**  某几位全局attention+窗口attention
**bigbird**  某几位全局attention+窗口attention+随机attention


提取句向量
**SimCSE**  batch内其他样本作为负样本，dropout后的自身作为正样本
**sentence-bert** 句子A、B编码后得到u，v，|u-v|，拼接起来预测01，之后取u做cosine
**bert-written**  （句向量本身是各向异性，cosine适用于标准正交基，因此将其变化成各向同性，即将数据集的向量变成均值为0，协方差矩阵为单位阵）




### Learning Confidence for Out-of-Distribution Detection in Neural Networks
https://arxiv.org/pdf/1802.04865.pdf

背景：添加一个head，可以输出模型的不确定程度，在不需要额外数据的情况下检测ood(不确定)数据

方法：新增一个预测结果c，大小为0-1，代表模型的不确定度，将模型的预测结果p改为 c*p+(1-c)*y，其中y是label。如果c=1，说明模型很确定自己的结果，如果c=0，说明完全不相信自己的结果，则将输出替换成label

为了防止c全部等于0，额外增加一个loss，比如-log(c)，c越小，loss越大，让模型自动去寻找一个平衡点。(测试的时候发现log(c)惩罚太大，模型容易让所有c都等于1，不加log效果会好一点)

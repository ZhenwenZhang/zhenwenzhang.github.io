---
title: "以QA形式解析Transformer和BERT"
---

随着NLP的不断发展，对Transformer和BERT相关知识的研究应用，也越来越细节，下面尝试用QA的形式深入不浅出Transformer和BERT。

> Transformer在哪里做了权重共享，为什么可以做权重共享？

> BERT的三个Embedding直接相加会对语义有影响吗？ 

> 在BERT中，token分3种情况做mask，分别的作用是什么？ 

> 为什么BERT选择mask掉15%这个比例的词，可以是其他的比例吗？ 

> 为什么BERT在第一句前会加一个[CLS]标志? 

> 使用BERT预训练模型为什么最多只能输入512个词，最多只能两个句子合成一句？ 

**1.Transformer在哪里做了权重共享，为什么可以做权重共享？**

Transformer在两个地方进行了权重共享：

1.Encoder和Decoder间的Embedding层权重共享；
2.Decoder中Embedding层和FullConnect（FC）层权重共享。

对于第一点，《Attention is all you need》中Transformer被应用在机器翻译任务中，源语言和目标语言是不一样的，但它们可以共用一张大词表，对于两种语言中共同出现的词（比如：数字，标点等等）可以得到更好的表示，而且对于Encoder和Decoder，嵌入时都只有对应语言的embedding会被激活，因此是可以共用一张词表做权重共享的。

https://mp.weixin.qq.com/s?__biz=MzIwMTc4ODE0Mw==&mid=2247513302&idx=2&sn=a65b802d0695a896652fa4b76ec02596&chksm=96ea6b56a19de2401e1ce5cca3bb50fd55bbdd38883b50bac985cd6521d1aa3b3f07f37b39d6&scene=126&sessionid=1604277667&key=6def13d9b1a9ecc5cb2c7dc1b6b732d56fe3b714281b652a02daa3a139cff58b0e452d8d35125ba9e5d8ad6234e20cd83d00e31a55702da326f416dcace2a2f46f56b56843bdc8183b5cab71756221d5b635d0ff18f28401c799443913fe252c165327b6e224e57efe65bdc7d12789cc27f414c0c712fb67cfee559db0bf6014&ascene=1&uin=Mjg2NTM2ODUyNA%3D%3D&devicetype=Windows+10+x64&version=63000039&lang=zh_CN&exportkey=AVsQ8nOppNP47SDEKiiBQh8%3D&pass_ticket=WbXX4kKIW2X89sE3D4KoL1hVzGtWpJDoL6zV4NSS%2F3f1DblAAn5pwhfT3AzkEy18&wx_header=0
---
layout: stacked
title: Stacked Attention Networks for Image Question Answering
date: 2019-11-22 17:04:45
tags:
---

### [Stacked Attention Networks for Image Question Answering](https://arxiv.org/pdf/1511.02274.pdf)


##### 概述

这篇论文提出了stacked attention networks (SANs)，可以使用自然语言查询图片中答案相关区域，并在四个image QA数据集上取得了优越的成绩。与NLP的QA不同的是，图像的QA是根据图片内容来对自然语言进行回答。通常的方法是分别对图片和文本提取特征，然后将他们结合来推断答案。

##### 任务描述

以论文中的例子来描述任务，给定：
- 一张图片：![image](/uploads/d66228ad4f73fc1e3636c0ce3500a3ef/image.png)
- 一个问题：what are sitting in the basket on a bicycle?

#### 模型部分

模型部分分为三部分，分别是图像建模，文本建模以及核心的stacked attention networks。
1. 图像建模

在这部分采用了传统的CNN结构进行建模，将图像进行卷积并取pooling后的输出作为图片的建模结果，得到向量$`f_I `$，为了统一维度，这里还进行了一步：$`v_I=tanh(W_I f_I+b_I)`$

2. 文本建模

在这部分中文章使用了两种方式，分别是：

1）使用LSTM对句子进行处理，对于一句Question  q=[$`q_1, q_2, ..., q_T`$]形成一个$`v_Q`$对该句子进行表示。这里词语先采用one hot编码然后使用$`x_t=W_e q_t`$映射到向量空间中然后丢入LSTM。

2）使用CNN对句子进行处理，对于一句Question，与LSTM不同的是，直接将词向量进行拼接（这里$`x_t`$和上一步相同）。然后采用三种尺寸的filter去卷，分别是1，2，3，对应unigram，bigram和trigram。然后和常见的卷积网络类似，采用最大池化。

这一步中对于文本的表示我们用$`v_Q`$进行表示。

3. Stacked Attention Networks Given

对于前两步得到的$`v_I`$和$`v_Q`$，首先将他们丢到一个简单的网络层中，然后通过softmax生成图像区域上的注意力分布，见下图：

![image](/uploads/e464ef434278bc1ce6af922a03c4ae30/image.png)

其中，$`v_I`$的维度是`d*m`，$`v_Q`$的维度是`d`，这里d是图像尺寸，m是图像区域数。最终得到的$`p_I`$是一个m维的向量，用于表示对应于给定$`v_Q`$的每个图像区域的注意力概率。

根据注意力分布，计算来自一个区域每个图像矢量的加权和，然后将其与$`v_Q`$进行结合（见下图）

![image](/uploads/232c4d1f0880dc6cf1539e2793821aa9/image.png)

这种做法的牛逼之处在于结合了问题信息和潜在答案的视觉信息，比简单将图像和文本句子信息组合更厉害。

但是，作者指出，对于复杂问题，一层attention层不足以得到正确的答案，因此作者使用了多层的attention，每层都会尽可能提取细粒度的信息，对于第k层，采用如下的计算方式：

<center>![image](/uploads/9c2c70ee406240ad54e081cc1719354d/image.png)</center>

不断将新得到的向量叠加在之前得到的向量上：

<center>![image](/uploads/a5b4b305e461f2cc20ce70e2497d240f/image.png)</center>

最终，重复K次操作，再接一个softmax得到最终的输出：

<center>![image](/uploads/9f81a96ee87bfaf2983c1fe1743b7551/image.png)</center>

##### 实验部分

作者对于图像建模使用了VGGNet；对于文本建模部分，由于实验有多个数据集，作者对于不同的数据集采用了不同的参数；对于attention部分，作者使用了两层attention，并且发现当大于等于3层的时候多层attention并没有什么卵用。

###### 论文中的示例图

![image](/uploads/05998e9676ad1d76f0d249190fb83c2c/image.png)




---
title: 训练中文spacy模型
date: 2019-01-22 12:23:30
tags:
    - PyTorch
    - NLP
    - 学习
description: train and modify the neural coreference model, use PyTorch
top: 1
---

### 准备工作

- 安装(conda)
  - 列出已有的虚拟环境: 
        
        conda env list
  - 创建新的环境：

        conda create -n py27-torch python=2.7

  - 激活/关闭环境

        source activate py27-torch
        source deactivate
  - 安装PyTorch
      ```
      conda install pytorch torchvision -c pytorch

      由于服务器无外网链接，因此采用离线安装的方法，下载https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/linux-64/pytorch-1.0.0-py2.7_cuda9.0.176_cudnn7.4.1_1.tar.bz2
      
      然后执行：
      conda install --offline pytorch-1.0.0-py2.7_cuda9.0.176_cudnn7.4.1_1\ \(1\).tar.bz2
      ```

- 所需条件（[来自作者的简介](https://github.com/huggingface/neuralcoref/blob/master/neuralcoref/train/training.md#train-on-a-new-language)）
  - parser to parse chinese
  - pre-trained word vector
  - conll format files

### 安装NeuralCoref

    git clone https://github.com/huggingface/neuralcoref.git
    cd neuralcoref
    pip install -e .
    (注：上面e后面有个小数点)

### 进行训练


![image](/spacy-learning/1.png)

遇到问题

![image](/spacy-learning/2.png)
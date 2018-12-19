---
title: TF入门——使用线性回归进行实验
date: 2018-12-10 21:39:33
tags:
	- Tensorflow
description: TF入门——使用线性回归进行训练
top: 1
---

### 思路

首先，我们通过random构建一部分数据，这里随机了1000个数据构建一个一维数组作为输入，y_true随机取0或者1。然后使用sklearn的[train_test_split](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)函数进行划分，在本例子中使用0.1的比例进行划分。划分后的数据shape如下图所示：
![image](/learning-tensorflow-linear-regression/1.png)
然后我们定义了进行预测的公式（y = w * x + b)，使用[均方误差](https://baike.baidu.com/item/%E5%9D%87%E6%96%B9%E8%AF%AF%E5%B7%AE)作为损失函数，使用梯度下降对loss进行优化学习。然后定义epoch数，因为数据量比较小，所以这里也没有分batch进行学习。


### 代码

	# encoding: utf-8
	import tensorflow as tf
	import numpy as np
	import matplotlib.pyplot as plt
	from sklearn.model_selection import train_test_split
	
	# 一些定义
	number_of_data = 1000   # 数据总数
	test_size = 0.1 # 测试集占比0.1
	
	# 准备数据，划分训练集和测试集
	X_ = np.random.rand(number_of_data)
	y_ = np.array([np.random.choice([0,1]) for _ in range(number_of_data)])
	X_train, X_test, y_train, y_test = train_test_split(X_, y_,test_size=test_size)
	
	X = tf.placeholder(tf.float32)
	Y = tf.placeholder(tf.float32)
	
	W = tf.Variable(np.random.randn(), name="weight")
	b = tf.Variable(np.random.rand(), name="bias")
	
	# 1. 定义pred的函数
	pred = tf.add(tf.multiply(W, X), b)
	# 2. 定义loss
	train_size = X_train.shape[0]   # 即训练集数据的个数
	loss = tf.reduce_sum(tf.pow((pred - Y), 2)) / (2 * train_size)
	
	# 3. 定义优化器，这里使用梯度下降
	learning_rate = 0.01    # 定义学习率
	optimizer = tf.train.GradientDescentOptimizer(learning_rate).minimize(loss)
	
	# 初始化以上的内容
	init = tf.global_variables_initializer()
	
	# 创建图
	epoch_num = 1000    # 定义epoch
	with tf.Session() as sess:
	    sess.run(init)
	    for epoch in range(epoch_num):
	        for (x, y) in zip(X_train, y_train):    # 这里没有使用mini batch学习
	            sess.run(optimizer, feed_dict={X: x, Y: y})
	
	        if epoch % 50 == 0:
	            dev_loss = sess.run(loss, feed_dict={X: X_train, Y: y_train})
	            print("Epoch: ", epoch, end='')
	            print(" Loss: ", dev_loss, end='')
	            print(" W: ", sess.run(W), " b: ", sess.run(b))


### 输出

**运行时输出**
![image](/learning-tensorflow-linear-regression/2.JPG)

**loss变化**
![image](/learning-tensorflow-linear-regression/3.png)
由于这组数据没有什么实际的意义，因此没啥可解释的，可以看到loss很快下降并且很快就趋于稳定
---
title: textCNN 学习笔记
date: 2018-12-06
tags:
	- python
	- Tensorflow
	- NLP
top: 1
description: 学习textCNN的随笔
---

### 参考资料：

- [cnn-text-classification-tf-github](https://github.com/dennybritz/cnn-text-classification-tf)
- [Implementing a CNN for Text Classification in TensorFlow](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/)

### 卷积的过程

根据网上很流行的图片来说：
![image](/cnn/3-4.png)

假设我们有这么一句话**“I like this movie very much!”**包含标点符号一共有7个词语，如果对于每个词语我们使用5维的向量进行表示，那么这句话可以表示为7x5的矩阵，所以此矩阵我们作为输入。然后我们可以使用不同尺寸的卷积核来进行，比如图里使用了尺寸分别为2，3，4来做，每种又包含两种（这里猜测是指通道数，比如图像有RGB所以会有三个）。故使用不同的卷积核会产生2x3=6个向量，然后我们可以选择最大池化或者平均池化的方法得到一个一维向量，再将6个拼凑起来。得到的这个向量（图中五颜六色的）我们可以理解为从不同的角度对文本提取出的特征，然后接全连接&softmax层得到最终的分类的结果。

因此程序的思路就是首先定义cnn的网络结构，确定各个超参数，先构建词典从而对文本进行向量化，然后定义输入输出的接口，根据卷积核的尺寸和通道数定义卷积层，使用最大池化及ReLU激活。将数据划分训练集和验证集后，使用训练集构建batch iters进行训练。

### 数据样式

![image](/cnn/data.JPG)


---

### 代码

### train.py

	def preprocess():
	    """
	    切分数据
	    """
	    x_, y_ = data_helper.load_data_and_labels(tuple_datas)
	
	    # 构建词典，取所有的文本中最大的长度作为最大长度
	    max_document_length = max([int(len(x.split(" ")))for x in x_])  # 19
	
	    # 根据最大长度初始化字典
	    vocab_processor = learn.preprocessing.VocabularyProcessor(max_document_length)
	
	    # 将文本填充到字典中，下面一行等于注释的那两行，其中fit_transform()方法会返回一个迭代器
	    # fit_transform() 后，vocab_processor的vocabulary_包含几个重要的属性：_freq(即每个字的出现频率), _mapping(每个字对应的id)
	    x = np.array(list(vocab_processor.fit_transform(x_)))
	    # t = vocab_processor.fit_transform(x_)
	    # x = np.array(list(t))
	
	    # 取随机种子并打乱数据
	    np.random.seed(100)
	    shuffle_indices = np.random.permutation(len(y_))
	    x_shuffled = np.array(x)[shuffle_indices]
	    y_shuffled = np.array(y_)[shuffle_indices]
	
	    # 根据验证集的比例确定验证集的index
	    dev_sample_index = -1 * int(FLAGS.dev_sample_percentage * float(len(y_)))
	
	    # 划分训练集和验证集
	    x_train, x_dev = x_shuffled[:dev_sample_index], x_shuffled[dev_sample_index:]
	    y_train, y_dev = y_shuffled[:dev_sample_index], y_shuffled[dev_sample_index:]
	
	    # 手动删除无用的变量确保不会占用大量内存
	    del x, y_, x_shuffled, y_shuffled
	    return (x_train, y_train, x_dev, y_dev, vocab_processor)

fit_transform后的vocab_processor如下图所示：
![image](/cnn/vocab.JPG)


定义训练过程
	
	def train(x_train, y_train, x_dev, y_dev, vocab_processor):
	    # 创建图以及会话
	    with tf.Graph().as_default():
	        session_conf = tf.ConfigProto(
	            allow_soft_placement = FLAGS.allow_soft_placement, # 是否打印设备日志
	            log_device_placement = FLAGS.log_device_placement, # 若指定的设备不存在，是否允许自动分配设备
	        )
	        sess = tf.Session(config=session_conf)
	
	        with sess.as_default():
	            cnn_para = (
	                x_train.shape[1],
	                y_train.shape[1],   # num_classes, 2
	                len(vocab_processor.vocabulary_), # vocab_size
	                FLAGS.embedding_dim,    # emb size
	                list(map(int, FLAGS.filter_sizes.split(','))),
	                FLAGS.num_filters,  # 128
	                FLAGS.l2_reg_lambda,
	                vocab_processor
	            )
	            cnn = CNN(cnn_para)
	
	        global_step = tf.Variable(0, name = "global_step", trainable = False)   # 这里trainable是false
	
	        # 定义优化器
	        optimizer = tf.train.AdamOptimizer(1e-3)    # 括号内是学习率，使用ADAM优化器
	        grads_and_vars = optimizer.compute_gradients(cnn.loss)  # 计算梯度
	        train_op = optimizer.apply_gradients(grads_and_vars, global_step = global_step) # 应用梯度
	
	        # 输出的文件夹
	        timestamp = str(int(time.time()))
	        out_dir = os.path.abspath(os.path.join(os.path.curdir, 'runs', timestamp))
	        print('输出文件夹：', out_dir)
	
	        # checkpoint 目录
	        checkpoint_dir = os.path.abspath(os.path.join(out_dir,'checkpoints'))
	        checkpoint_prefix = os.path.join(checkpoint_dir,'model')
	        if not os.path.exists(checkpoint_dir):
	            os.makedirs(checkpoint_dir)
	        saver = tf.train.Saver(tf.global_variables(), max_to_keep = FLAGS.num_checkpoints)  # 保存器
	        
	        # 写入字典
	        vocab_processor.save(os.path.join(out_dir, "vocab"))
	
	        # 初始化向量
	        sess.run(tf.global_variables_initializer())
	        
	        def train_step(x_batch, y_batch):
	            feed_dict = {
	                   cnn.input_x: x_batch,    # 对应placeholder
	                   cnn.input_y: y_batch,
	                   cnn.dropout_keep_prob: FLAGS.dropout_keep_prob
	                   }
	
	            temp, step, loss, accuracy = sess.run(
	                    [train_op, global_step, cnn.loss, cnn.accuracy],
	                    feed_dict
	                    )
	            time_str = datetime.datetime.now().isoformat()
	            print(time_str, step, loss,accuracy)
	
	        # 创建batch
	        batches = data_helper.batch_iter(
	                    list(zip(x_train, y_train)),
	                    FLAGS.batch_size,
	                    FLAGS.num_epochs
	                )
	        for batch in batches:
	            x_batch, y_batch = zip(*batch)
	            train_step(x_batch, y_batch)
	            current_step = tf.train.global_step(sess, global_step)
	            
	            if current_step % FLAGS.checkpoint_every == 0:
	                path = saver.save(sess, checkpoint_prefix, global_step=current_step)
	                print('save the checkpoint to:   ',path)
	
调用方法：
	
	def main():
	    x_train, y_train, x_dev, y_dev, vocab_processor = preprocess()
	    train(x_train, y_train, x_dev, y_dev, vocab_processor)
	
	if __name__ == '__main__':
	    main()


---
### data_helper.py

定义产生batch的方法

	def batch_iter(data, batch_size, num_epochs, shuffle=True):
	    data = np.array(data)
	    print(len(data))
	    data_size = len(data)
	    num_batches_per_epoch = int((len(data) - 1)/batch_size) + 1 # 每个epoch有多少个batch
	    for epoch in range(num_epochs):
	        if shuffle:
	            shuffle_indices = np.random.permutation(np.arange(data_size))
	            shuffled_data = data[shuffle_indices]
	        else:
	            shuffled_data = data
	
	        for batch_num in range(num_batches_per_epoch):
	            start_index = batch_num * batch_size
	            end_index = min((batch_num + 1) * batch_size, data_size)    # 如果end index超过了最大，则选择最大的那个
	            yield shuffled_data[start_index: end_index]



---
### CNN_Network.py

	class CNN(object):
	    def __init__(self, cnn_para):
	        """
	        :param cnn_para:装在CNN网络的参数，是个tuple
	        """
	        print('创建CNN网络中......')
	        print('CNN参数设置：')
	        print('seq_length:', cnn_para[0])
	        print('num_classes', cnn_para[1])
	        print('vocab_size:', cnn_para[2])
	
	        sequence_length = cnn_para[0]
	        num_classes = cnn_para[1]
	        vocab_size = cnn_para[2]
	        embedding_size = cnn_para[3]
	        filter_sizes = cnn_para[4]
	        num_filters = cnn_para[5]
	        l2_reg_lambda = cnn_para[6]
	        vocab_processor = cnn_para[7]
	
	        # 构建输入输出层、dropout
	        # 案例中self.input_x 的shape为(?, 19)
	        # self.input_y 的shape为(?, 2)
	        self.input_x = tf.placeholder(tf.int32, [None, sequence_length], name = 'input_x')
	        self.input_y = tf.placeholder(tf.float32, [None, num_classes], name = 'input_y')
	        self.dropout_keep_prob = tf.placeholder(tf.float32, name = "dropout_keep_prob")
	
	        # 定义l2 loss
	        l2_loss = tf.constant(0.0)
	
	        # 定义char embedding层
	        with tf.device('/cpu:0'), tf.name_scope('embedding'):
	            all_char_emb = [np.random.rand(300)]    # 初始化，必须先放进去一个，作为UNK，也就是说这个就是UNK的embedding
	            for k, v in vocab_processor.vocabulary_._mapping.items():
	                try:
	                    char_emb = list(char_emb_moedl[k]) # 这里可以改成别的embedding
	                except KeyError:
	                    char_emb = list(np.random.rand(300))
	                all_char_emb.append(char_emb)
	            # 每个字都被用一个300d的数组表示，由于一共有2180个字，因此all_char_emb的shape为(2180, 300)
	            all_char_emb = np.array(all_char_emb)
	
	            # 由于在此处使用embedding的每一维作为特征，因此构建W矩阵存放权重
	            self.W = tf.Variable(all_char_emb, name = "W", dtype = tf.float32)
	
	            # 执行下面两句后，self.embedding_chars的shape为(?, 19, 300)
	            # self.embedding_chars_expanded的shape为(?, 19, 300, 1)
	            self.embedding_chars = tf.nn.embedding_lookup(self.W, self.input_x)
	            self.embedding_chars_expanded = tf.expand_dims(self.embedding_chars, -1)    # 添加一维
	
	            # 初始化变量
	            tess = tf.Session()
	            tess.run(tf.global_variables_initializer())
	
	        # 定义卷积&池化层
	        pooled_outputs = []
	        for i, filter_size in enumerate(filter_sizes):
	            with tf.name_scope("conv-maxpool-%s" % filter_size):
	
	                # 卷积
	                filter_shape = [filter_size, embedding_size, 1, num_filters]
	                # filter_shape = [filter_size, 300, 1,128]
	                W = tf.Variable(tf.truncated_normal(filter_shape, stddev=0.1, name = "W"))
	                # W 的shape：[filter_size, 300, 1, 128]
	                b = tf.Variable(tf.constant(0.1, shape=[num_filters]), name="b")
	                # b 的shape：[128]
	
	                conv = tf.nn.conv2d(
	                    self.embedding_chars_expanded,
	                    W,
	                    strides = [1,1,1,1],
	                    padding = "VALID",
	                    name = "conv"
	                )
	
	                # 激活
	                h = tf.nn.relu(tf.nn.bias_add(conv, b), name = "relu")
	
	                # 池化
	                pooled = tf.nn.max_pool(
	                    h,
	                    ksize=[1, sequence_length - filter_size + 1, 1, 1],
	                    strides=[1,1,1,1],
	                    padding="VALID",
	                    name="pool"
	                )
	                pooled_outputs.append(pooled)
	
	        # 结合所有的池化特征
	        num_filters_total = num_filters * len(filter_sizes)
	        # 2个卷积核，3个卷积，因此产生6维的向量 #update:说的不对，这里是128 * 3 = 384
	
	        self.h_pool = tf.concat(pooled_outputs, 3)  # TODO:what??
	        self.h_pool_flat = tf.reshape(self.h_pool, [-1, num_filters_total]) # -1表示这个维度不指定，由程序自己计算生成
	
	        # 添加dropout
	        with tf.name_scope("dropout"):
	            self.h_drop = tf.nn.dropout(self.h_pool_flat, self.dropout_keep_prob)
	
	        # TODO：定义输出层？ | 最终（未正则化）的分数&预测
	        with tf.name_scope("output"):
	            W = tf.get_variable(
	                "W",
	                shape=[num_filters_total, num_classes],
	                initializer=tf.contrib.layers.xavier_initializer()
	            )
	            b = tf.Variable(tf.constant(0.1, shape=[num_classes]),name = "b")
	            l2_loss += tf.nn.l2_loss(W) # 返回的是一个数值
	            l2_loss += tf.nn.l2_loss(b)
	            self.scores = tf.nn.xw_plus_b(self.h_drop, W, b, name="scores") # TODO:what's this
	            self.predictions = tf.argmax(self.scores, 1, name="predictions")
	
	        # 计算交叉熵 # TODO:看懂这几个函数的意思
	        with tf.name_scope("loss"):
	            losses = tf.nn.softmax_cross_entropy_with_logits(
	                logits=self.scores,
	                labels=self.input_y
	            )
	            self.loss = tf.reduce_mean(losses) + l2_reg_lambda * l2_loss
	
	        # 精确度 # TODO: reduce mean
	        with tf.name_scope("Accuracy"):
	            correct_predictions = tf.equal(self.predictions, tf.argmax(self.input_y, 1))
	            self.accuracy = tf.reduce_mean(tf.cast(correct_predictions, "float"), name="accuracy")
	
	        print('Create CNN network success!')



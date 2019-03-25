---
title: about
date: 2018-11-29 11:30:30
---

男，94年生，现居北京。


- 本科(2012.9-2016.6) 信息工程学院 智能科学与技术
- 硕士(2016.9-2019-6) 信息工程学院 软件工程
- 联系方式:  candnes@sina.com
- 技能：
	- python(PyCharm Debugger/Jupyter notebook)
	- Git/Linux
	- Django/BeautifulSoup
	- Tensorflow/Sklearn
	- Office/Markdown
- 个人兴趣：
	- NLP相关
	- 中文指代消解研究 (可参考：[指代消解基础](https://junzx.github.io/2018/04/24/%E6%8C%87%E4%BB%A3%E6%B6%88%E8%A7%A3%E5%9F%BA%E7%A1%80/) )
	- 数据挖掘/推荐/决策
- 爱好：游泳/看书/摄影/Minecraft
- 希望在生产生活中使用所学技能，认同技术落地


## **项目经历**

**基于协同过滤的图书推荐系统 (2015.09-2016.6)**

任务：利用图书的标签和用户的信息对用户进行图书推荐。

工作：
- 使用python&re爬取豆瓣图书的数据；
- 根据用户的阅读历史及属性构建user profile；
- 使用K-means算法对用户进行聚类；
- 预测当前用户对每本待推荐图书的打分；
- 对某个用户找到其相似用户并进行推荐。

涉及技术：协同过滤、K-means

**中文指代消解问题研究 (2017.12-2018.10)**

任务：使用CoNLL2012中文数据集，对文本预处理，抽取待消解项，构建消解系统。使用其他方法提升消解的性能。

工作：
- 对文本进行预处理，进行分词、词性标注等工作。使用NLTK提取文本中候选表述；
- 利用语言学的规则构建消解系统，对于提取出的表述进行分析和判别；
- 构建卷积神经网络，对词语属性进行判别分类；
- 将分类结果应用于代词消解上，提升代词消解的性能。

贡献：
- 构建了一个完整的中文指代消解系统
- 使用Bi-LSTM-CRF提升表述提取的准确率
- 使用分类器对词语属性分类，提升代词消解结果

涉及技术：文本分析工具(StanfordCoreNLP/NLTK)、python、tensorflow、textCNN

## **实习经历**

**北京阿博茨科技有限公司 - 算法中心 - 自然语言处理实习生**

参与公司金融信息抽取平台项目的研发，跟进项目进度，根据需求完成工作

- 对业务进行整理，形成文档
- 对数据进行分析及清洗
- 对文本进行依存关系分析及机器学习算法进行分类
- 负责项目中信息推理的部分实现
- 完成其他需要的工作

## **成果**

- 发表论文
> Zhu Y. A book recommendation algorithm based on collaborative filtering[C]. international conference on computer science and network technology, 2016: 286-289.(EI: 20180104610894)
>
> Zhu Y, Song W, Liu L, et al. Collaborative Filtering Recommender Algorithm Based on Comments and Score[C]. international symposium on computational intelligence and design, 2017.(EI: 20182105218451)
>
> Improving Anaphora Resolution by Animacy Identification. （检索中）

- 软件著作权
> 基于协同过滤的图书推荐系统V1.0(2016SR333795)







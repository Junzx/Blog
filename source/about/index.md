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

任务：
- 利用图书的标签和用户的信息对用户进行图书推荐。

工作：
1. 数据获取：从豆瓣爬取部分图书及用户数据并进行清洗；
2. 用户建模：根据用户属性描述用户偏好；
3. 用户聚类：使用K-means算法对用户进行聚类；
4. 推荐：对某个用户找到其相似用户；根据这些用户喜好推荐。

涉及技术：协同过滤、K-means

**中文指代消解问题研究 (2017.12-2018.10)**

任务：
- 使用CoNLL2012中文数据集，对文本预处理，抽取待消解项，构建消解系统；
- 对中文文本属性识别构建分类器，提升代词消解性能。

工作：
1. 文本处理：进行分词、词性标注、命名实体识别等工作；
2. 表述提取：根据句法树使用N LT K.Tree提取表述；
3. 指代消解：利用语言学的规则构建消解系统，对于提取出的表述进行分析和判别；
4. 改进：对词语属性进行判别分类；将分类结果应用于代词消解上，提升代词消解的性能。

贡献：
- 构建了一个完整的中文指代消解系统；
- 使用Bi-LSTM-CRF提升表述提取的准确率；
- 使用分类器对词语属性分类，提升代词消解结果。

涉及技术：文本分析工具(StanfordCoreNLP/NLTK)、python、Tensorflow、textCNN

## **实习经历**

**北京阿博茨科技有限公司 - 算法中心 - 自然语言处理实习生**

参与公司金融信息抽取平台项目的研发，跟进项目进度，根据需求完成工作

职责：
- 参与公司金融领域信息抽取平台的开发，跟进项目进度，根据需求完成工作。
- 该平台针对上市公司文档，抽取有用信息形成简报，方便使用者快速了解文档内容。
- 其中待抽取信息分为以下四类
	1. 抽取部分：使用正则表达式直接从文档抽取
	2. 抽取+判别部分：从文档抽取多个候选，进行分类判定
	3. 推理部分：根据文档对1和2的信息进行重组或者计算
	4. Summary部分：总结模板形成summary

工作
- 对业务逻辑进行整理，形成文档
- 负责项目中推理部分和Summary部分的实现以及部分抽取+判别任务的研究。（3、 4以及部分2）

## **成果**

- 发表论文
> Zhu Y. A book recommendation algorithm based on collaborative filtering[C]. international conference on computer science and network technology, 2016: 286-289.(EI: 20180104610894)
>
> Zhu Y, Song W, Liu L, et al. Collaborative Filtering Recommender Algorithm Based on Comments and Score[C]. international symposium on computational intelligence and design, 2017.(EI: 20182105218451)
>
> Improving Anaphora Resolution by Animacy Identification. （检索中）

- 软件著作权
> 基于协同过滤的图书推荐系统V1.0(2016SR333795)







---
title: 2019日记&日报
date: 2019-01-02 16:26:08
tags:
    - 随笔
description: 用来记录每天的工作-2019
top: 70
---


###          January   2019          
Sun | Mon | Tue  | Wed | Thu | Fri | Sat 
---| ---| ---| ---| ---| ---| ---|
  |  | 1 | [2](#12) | [3](#13) | 4 | 5 |
 6 | [7](#17) | [8](#18) | [9](#19) | [10](#110) | 11 | 12 |
 [13](#113) | 14 | 15 | [16](#116) | [17](#117) | [18](#118) | [19](#119) |
 [20](#120) | [21](#121) | [22](#122) | [23](#123) | [24](#124) | [25](#125) | [26](#126) |
 27 | [28](#128) | 29 | 30 | 31 |

**本月主要任务：**

- 完成毕设的所有实验程序
- 完成毕设论文的开头部分
- 更新简历、准备春招
- 保证每天的打卡

---
 **<span id="12">1-2</span>**

 - 制定[19年计划](https://junzx.github.io/2019/01/02/year-plan/)

---
**<span id="13">1-3</span>**

- 由于博客搬家，暂时停更

---
**<span id="17">1-7</span>**

- 完成博客迁移的工作
- 过了一遍论文

---
**<span id="18">1-8</span>**

- 收集到了几个有用的数据集
- 完成前两个sieve
- 明天预计完成所有的sieve

---
**<span id="19">1-9</span>**

- 除了sieve6之外都完成了
- 明天预计解决已完成的中一些bug，打好log
- 准备春招

---
**<span id="110">1-10</span>**

- Multisieve-bug-fix -关于get_modifier
- 画set coref的逻辑图

---
**<span id="113">1-13</span>**

**下周计划**

- 毕设前几章
- 买无印日程本
- 程序完成PRF评价部分
- 程序完成剩余的sieve部分

---
**<span id="116">1-16</span>**

- 尝试使用BiLSTM构建一个mention detection的程序
- 解决部分消极情绪

---
**<span id="117">1-17</span>**

- 买到了日程本，review之前的计划
- 整理了之前写的排序的笔记，合并为：[算法入门——python实现部分排序](https://junzx.github.io/2018/12/12/algorithm-learning-sort/)

---
**<span id="118">1-18</span>**

- 添加调用计算prf的perl程序，增加调用接口函数

---
**<span id="120">1-20</span>**

今日成果
- bug fix：解决将结果写入文件的问题

明日计划
- 完成论文第二章
- 看剩下的几个sieve的论文

---
**<span id="121">1-21</span>**

今日成果
- 解决linux下hexo博客更新的问题，之前的问题是g、s均正常，但是deploy不正常，后将Blog下.deplot_git手动清除后d成功
- 完成论文第二章的一半，后面需要继续看论文然后完善
- 完成调用scorer.pl的函数，实现绘图的工具
- 增加了几个sieve，主要是采用之前项目的代码

明日计划
- 关注待学习的课程，制定相应的计划
- 完成论文第三章

---
**<span id="122">1-22</span>**

今日成果
- 训练中文spacy: https://junzx.github.io/2019/01/22/spacy-learning/
- 解决分支冲突的问题

    ```
    问题描述：
    
    clone Blog.git后，修改各md，然后执行add/commit/push可以正常push到Blog.git。但是当执行hexo d后，项目会被设置为“分支 master 设置为跟踪来自 git@github.com:Junzx/junzx.github.io.git 的远程分支 master。”，此时如果执行add/commit/push会将整个Blog.git push到github.io项目上。
    
    解决方案：
    如果想push Blog.git 应该使用“git push -u origin master”
    ```

- 由于之前[任务](https://github.com/huggingface/neuralcoref)未完成，没有写论文
  - https://github.com/huggingface/neuralcoref
  - https://github.com/huggingface/neuralcoref/blob/master/neuralcoref/train/training.md
  - https://medium.com/huggingface/how-to-train-a-neural-coreference-model-neuralcoref-2-7bb30c1abdfe

明日计划
- 去医院
- 完成论文第三章内容

---
**<span id="123">1-23</span>**

- bug fix & review

---
**<span id="126">1-26</span>**

- 参与北京GDG组织的TF入门CodeLab
- 收拾后天去南京的物品

---
**<span id="128">1-28</span>**

- 出发去南京，由于时间冲突，只去了明孝陵，晚上到达最终目的地



###         February   2019          
Sun | Mon | Tue  | Wed | Thu | Fri | Sat 
---| ---| ---| ---| ---| ---| ---|
  |  |  |  |  | 1 | 2 |
 3 | [4](#24) | 5 | 6 | [7](#27) | [8](#28) | [9](#29) |
 [10](#210) | 11 | 12 | 13 | 14 | 15 | 16 |
 17 | [18](#218) | [19](#219) | [20](#220) | [21](#221) | [22](#222) | [23](#223) |
 [24](#224) | [25](#225) | [26](#226) | [27](#227) | [28](#228) |



--- 
**<span id="204">2-04</span>**

- 祝大家猪年大吉
- 希望世界和平
- 希望一切顺利


--- 
**<span id="207">2-07</span>**

- 整理论文的实验，由于没有网络因此比较受限制

--- 
**<span id="210">2-10</span>**

- 整理实验发现，某sieve的p可到0.7，但是f始终稳定在0.5，需要解决

--- 
**<span id="218">2-18</span>**

- 更改论文提纲
- 考虑如果将prf为0的文档不作统计，效果可以提升0.2左右（每个sieve）

--- 
**<span id="219">2-19</span>**

- 写论文
- 将使用lstm提取mention的程序改用pre-trained embedding，遇到一点问题
  - FailedPreconditionError (see above for traceback): HashTable has different value for same key
  - 可能是参数问题，占用内存过大
- lstm遇到奇怪字符报错，如果用try跳过的话会有其他错误，暂未解决
- https://www.one-tab.com/page/VyQiRQjxQMeMcKVvdw_1JQ

--- 
**<span id="220">2-20</span>**

- 写论文，将论文从markdown转移到word模板中

--- 
**<span id="221">2-21</span>**

- 写论文，主要写multisieve部分
- 尝试运行django项目，发现有bug跑不起来，由于重构以后版本有较大变化，因此暂放

--- 
**<span id="222">2-22</span>**

- 写论文，计划明天彻底完成第二章
- 重新读相关论文，注意到：
	- 对于某个表述选择多个候选表述，在选择的时候不应该考虑候选表述是否是处理过的
	- 当从候选表述集合中找到共指的表述后，遍历应当停止
	- 在最后一步写入文件测评的时候，应该抛弃single cluster

--- 
**<span id="223">2-23</span>**

- 写论文，第二章未彻底完成，但已经完善大部分，明天完成CR的任务总结。计划圆满毕业后开源部分论文。

--- 
**<span id="224">2-24</span>**

- 测试perl的评价函数
	- document A和document B分别评价结果
	- 然后合成一个文件C进行评价
	- 结论：应该合成一个文件后进行评价
		- Precision: 66.76%
		- Recall：64.87%
		- f score：65.8%
- 写论文
	- 还是没完全完成第二章
	- 新增内容：语料资源+评价方法
	- 目前差新添加的内容和国外基于学习的研究现状
- 其他：
	- https://blog.csdn.net/muumian123/article/details/85616175
	- https://blog.csdn.net/Eastmount/article/details/48566671
	- https://www.jianshu.com/p/995cc0b8ebe5
	- https://www.jianshu.com/p/a74fa768594e

--- 
**<span id="225">2-25</span>**

- MUC（Message Understanding Conference）资源
	- https://cs.nyu.edu/cs/faculty/grishman/muc6.html
	- https://www.itl.nist.gov/iaui/894.02/related_projects/muc/proceedings/muc_7_toc.html
	- https://www-nlpir.nist.gov/related_projects/muc/
	- https://en.wikipedia.org/wiki/Message_Understanding_Conference
	- https://catalog.ldc.upenn.edu/LDC2001T02
	- http://aclweb.org/anthology/C96-1079（MUC6有用）
	- http://aclweb.org/anthology/M98-1029（MUC7有用）
	- https://dblp2.uni-trier.de/db/conf/muc/index.html
- ACE（Automatic Content Extraction）资源
	- https://en.wikipedia.org/wiki/Automatic_content_extraction
	- https://tac.nist.gov/publications/index.html（TAC）
	- http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.78.8442&rep=rep1&type=pdf
	- https://www.ldc.upenn.edu/collaborations/past-projects/ace
	- https://www.ldc.upenn.edu/collaborations/past-projects/ace/annotation-tasks-and-specifications
	- https://www.ldc.upenn.edu/collaborations/past-projects/ace/papers-and-presentations
	- https://www.ldc.upenn.edu/sites/www.ldc.upenn.edu/files/chinese-events-guidelines-v5.5.1.pdf
- OntoNotes数据
	- https://catalog.ldc.upenn.edu/docs/LDC2013T19/OntoNotes-Release-5.0.pdf
	- https://catalog.ldc.upenn.edu/LDC2013T19
- 论文
	- 完成对语料资源的总结，可扩写
	- 优先完成剩余内容

--- 
**<span id="226">2-26</span>**

- 写论文
	- 关于CNN部分，还可以继续扩写
	- 分配一点时间整理实验

--- 
**<span id="227">2-27</span>**

- 训练cnn模型，保存在：1551257180
- 怼进部分实验
- ！明天完成LSTM+CRF的部分


--- 
**<span id="228">2-28</span>**

今日安排：

- 测试cnn模型
- LSTM+CRF

今日完成：

- 修改简历
- 测试cnn参数
- 完成RNN及LSTM

明日安排：

- LSTM、CRF
- prf of animacy classifier 
- add animacy to pr

###         March   2019          
Sun | Mon | Tue  | Wed | Thu | Fri | Sat 
---| ---| ---| ---| ---| ---| ---|
  |  |  |  |  | [1](#31) | 2 |
 3 | 4 | [5](#35) | [6](#36) | [7](#37) | [8](#38) | [9](#39) |
 [10](#310) | 11 | [12](#312) | [13](#313) | [14](#314) | [15](#315) | 16 |
 17 | 18 | [19](#319) | [20](#320) | [21](#321) | [22](#322) | [23](#323) |
 [24](#324) | [25](#325) | [26](#326) | 27 | 28 | 29 | 30 |
 31 |

--- 
**<span id="31">3-1</span>**

I am not happy.

---
**<span id="35">3-5</span>**

- 发现了原来项目中存在很大的bug，主要集中在写入文件方法上，尝试fix，但由于过于耦合暂时放弃
- 在重构后的项目上进行实验，得到效果如下

		{'bcub': ('68.63%', '66.82%', '67.71%'),
		'blanc': ('34.78%', '66.84%', '45.75%'),
		'ceafe': ('76.51%', '56.09%', '64.73%'),
		'muc': ('82.84%', '74.71%', '78.56%')}

---
**<span id="36">3-6</span>**

- 完成指代消解所有程序

---
**<span id="37">3-7</span>**

- 惊天地泣鬼神的完成了使用句法树提取表述的程序，没有filter和ner的buff，效果拔群

		prf：
		0.363624747495
		0.985709876948
		0.503406182085
- 跑完LSTM，效果没有想象中的拔群
- 修改论文的目录安排

---
**<span id="38">3-8</span>**

- 论文完成 将第三章名称改为多模型

---
**<span id="39">3-9</span>**

- 将第三章名称改回多轮处理
- 完善每轮模型的描述
- 不知道将来工作交接给谁，其实我还是很希望把这个完善好的
- 尽快跑通django，但是笔记本带stanford的工具包带不动，难以本地调试

---
**<span id="310">3-10</span>**

- 重构论文
- 对于程序部分，考虑应该如何考虑实体的信息

---
**<span id="312">3-12</span>**

- 提交查重版本的论文
- 查重率为0.4%，通过

---
**<span id="313">3-13</span>**

- 解决了Mention Detection的bug

		{'bcub': ('26.9%', '57.76%', '36.7%'),
		'blanc': ('15.48%', '44.32%', '22.95%'),
		'ceafe': ('25.76%', '56.37%', '35.36%'),
		'muc': ('33.61%', '64.82%', '44.27%')}

- 完成Init数据的代码，构成了完整的指代消解系统

---
**<span id="314">3-14</span>**

- 完成性别属性识别对代词消解的提升
- Mention Detection好像有新bug

		{'bcub': ('19.52%', '65.17%', '30.05%'),
		'blanc': ('3.66%', '65.49%', '6.94%'),
		'ceafe': ('27.18%', '44.93%', '33.87%'),
		'muc': ('32.28%', '71.33%', '44.45%')}

---
**<span id="315">3-15</span>**

交接部分代码

---
**<span id="319">3-19</span>**

- 完成论文，提交系统
- 完成论文，提交学院
- 解决git上传过大文件的问题，用了原始的办法

---
**<span id="320">3-20</span>**
- 跑Django
	- 输入的文本回转化为unicode
	- stanford corenlp不能处理Unicode，需要先encode('utf-8') 
	- 准确来说，输入的是utf-8，但是分词完了输出的是Unicode列表
- Django发现原来程序在init部分有问题
- Multisieve-cr发现了较多bug，明天修复
- 参考：https://web.stanford.edu/~jurafsky/pubs/coli_a_00152.pdf
- 关于python的log：
  - https://zhuanlan.zhihu.com/p/38782314
  - https://docs.python.org/2/library/logging.handlers.html#filehandler

---
**<span id="321">3-21</span>**

- 解决bug的一天，包括但不限于：
  - 打log不完整
  - SubjectUtils.sieve_utils.py  get_candidate_mentions
  - SubjectUtils.sieve_utils.py  get_modifier
  - Experiment.ExperimentResult.load_mention_info_result.py 改为load json
  - Multisieve.exact_match.py 增加了确定字符串比较
  - Scorer.api_prf 改成写入log文件，不再print
  - 所有的print都用pprint工具
  - 将sieve order新建了一个config py
  - 基本保证py2、3跨平台
- 结论
  - 改版的修饰语提取方法更准一些
  - 选择候选先行语的方法影响不大，主要影响是句子距离的约束

---
**<span id="322">3-22</span>**

- 计划本周完成 ML实战的第一遍阅读
- 遇到决策树相关内容待深入了解
- 希望明天有好结果

---
**<span id="323">3-23</span>**

- 今天去笔试+面试，果然金融知识还比较欠缺，不过面试官很nice，期待下周结果
- 解决sieve_timer装饰器返回的函数丢失原函数名的问题
- 将exact match改为字符串精确匹配，发现效果尚可

			 Precision | recall | f1_score
		----------------------------------------
		bcub:      93.52    21.95    35.56
		ceafe:     63.29    26.74    37.60
		muc:       92.26    30.57    45.93
		blanc:     90.41    15.55    26.54
- 发现filter sieve用处不大，因为在写入文件的时候就会删掉single Mention

---
**<span id="325">3-25</span>**

- 快速过了一遍 ML实战 需要深入西瓜书/未完成的内容包括
  - numpy & 线性代数部分
  - 决策树、bagging、boosting、adaboost
  - 手推逻辑回归
  - k-means的k选择、二分k-means
  - PCA与word embedding
  - SVM
  - SVD与推荐
- 西瓜书线性模型、贝叶斯
- 更新自我介绍部分的内容：[about me](https://junzx.github.io/about/)

---
**<span id="326">3-26</span>**

参考链接

信息量、信息熵、条件熵、信息增益
- [知乎-通俗理解信息熵](https://zhuanlan.zhihu.com/p/26486223)


决策树(**TODO**)
- https://air-yan.github.io//MachineLearning/sv_trees_ch/
- [知乎-深入浅出理解决策树算法（一）-核心思想](https://zhuanlan.zhihu.com/p/26703300)
- [知乎-深入浅出理解决策树算法（二）-ID3算法与C4.5算法](https://zhuanlan.zhihu.com/p/26760551)
- [ID3、C4.5、CART、随机森林、bagging、boosting、Adaboost、GBDT、xgboost算法总结](https://zhuanlan.zhihu.com/p/34534004)
- [从决策树到随机森林：树型算法的原理与实现](https://zhuanlan.zhihu.com/p/28217071)
- [决策树算法的Python实现](https://zhuanlan.zhihu.com/p/20794583)

Note
见： 
https://junzx.github.io/2019/04/08/learning-nlp/
---
**<span id="327">3-27</span>**
- 讲决策树很清晰：https://zhuanlan.zhihu.com/p/26760551，包括ID3和C4.5
- bagging/boosting, GBDT/adaboost/XGBoost

###         April   2019          
Sun | Mon | Tue  | Wed | Thu | Fri | Sat 
---| ---| ---| ---| ---| ---| ---|
  | 1 | 2 | 3 | [4](#44) | 5 | 6 |
 7 | [8](#48) | [9](#49) | [10](#410) | [11](#411) | [12](#412) | [13](#413) |
 [14](#414) | [15](#415) | [16](#416) | [17](#417) | [18](#418) | [19](#419) | [20](#420) |
 [21](#421) | [22](#422) | [23](#423) | [24](#424) | [25](#425) | [26](#426) | [27](#427) |
 [28](#428) | [29](#429) | [30](#430) |

--- 
**<span id="44">4-4</span>**

最近真是忙成汪，趁着假期总结一下

- 尝试将项目分开成两部分，但是发现实际上没有意义
- 更新ConllDataLoader

--- 
**<span id="46">4-6</span>**

- 搞定HMM，有空上传笔记

--- 
**<span id="48">4-8</span>**

- https://junzx.github.io/2019/04/08/learning-nlp/
- https://junzx.github.io/2019/04/08/article-directory/
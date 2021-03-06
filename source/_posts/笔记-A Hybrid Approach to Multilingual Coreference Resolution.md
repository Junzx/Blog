---
title: 笔记-A Hybrid Approach to Multilingual Coreference Resolution
date: 2017-19-14
tags:
    - Coreference Resolution
    - NLP
description: 学习笔记
top: 1
---
#### Abstract

采用了一种混合方法来指代消解任务，结合了基于规则方法的优势和基于学习方法的优势。评分很高。

#### Section 1. Introduction

- 拓展了CoNLL2012中的任务，从单一语言→多语言。针对三种语言：英语、汉语、阿拉伯语。
- 针对这三种语言都设计了系统
- Four tracks：
    - closed track：for three languages
    - open track： for Chinese
- 有两个明显的特征：
    - 往年的用的是基于规则的方法**或**基于学习的方法，我们这回将他们的优势结合起来了。
    - 往年的人没有开发“genre-specific”信息，我们对我们系统参数做出了优化，遵守了每个genre。
- 我们采用混合方法的原因是因为rule-based method 和learning-based method都有唯一的长处。
- 根据上届CoNLL任务的方法，可以采用一个简单规则的公平小集合。
- 我们先前的在用ml方法解决指代消解任务的工作，可以在启发词汇特征，优化XXXX  **这段没懂**
- 在本系统中，采用正常的架构来完成实体检测任务（在消解之前），‘期望评价方法’这两个组件被充分利用。
- 本篇论文的布局安排：
    - mention detection conponent(Section2)
    - coreference resolution component(Section3)
    - show how their parameters are jointly optimized(Section4)/展示决定因素是如何优化的
    - 评估&实验（Section5）

#### Section 2. Mention Detection

- 为了保证准确率和召回率的平衡，我们采用了一种**两步走**的方法。——"extraction step" & "pruning step"
    - 首先，在*extraction step* 中，我们**定位命名实体**，**采用启发式"language-specific"方法来提取mentions**，以上工作从一个句法分析树，尽量增加召回率。
    - 然后，在*pruning step*中，我们**采用启发式language-specific剪枝和基于学习的language-independent剪枝**。
    - 总结，在step1中，定位实体，提取mention，增加召回率。在step2中，采用基于启发式和基于学习的剪枝
- Heuristic Extraction and Pruning（启发式提取和剪枝）
    - 英语：
        - 在提取工作中，我们从相邻文本**span s**中创建候选mention，如果span s满足：
            1. s是一个在句法分析树种的PRP或者NP
            2. s作为一个NE，但不是PERCENT，MONEY，QUANTITY或者CARDINAL
        - 在剪枝工作中，我们将移除一个候选mention mk，如果mk满足：
            1. mk夹在一个很大的mention mj中，并且这个mk和mj有共同的头部
            2. mk有一个量词或者一个表示部分的修饰语
            3. mk是一个单数常见NP，我们保留与时间有关的mention（例如today）
    - 中文
        - 在提取工作中，我们从句法树中的所有NP，QP结点创建中文mention
        - 在剪枝工作中，我们将移除一个候选mention mk，如果mk满足：
            1. mk夹在一个很大的mention mj中，并且这个mk和mj有共同的头部。除非如果mk和mj在一篇新闻通信中。不像其他的文件标注，中文新闻通信文档注释确实考虑了这些共指对。
            2. mk是一个NE，比如说PERCENT，MONEY，QUANTITY和CARDINAL
            3. mk是一个疑问代词，例如what，where
    - 阿拉伯
        - 略
- Learning-Based Pruning（基于学习的剪枝）
    - 当启发式方法定位了候选mention后，还不能确定这个候选mention就是可以共指的。为了增强剪枝效果（因此~mention detection的准确率），我们采用了基于学习的方法来剪枝。
    - 描述：我们用train data来定位和随后丢弃这些可能不能共指的候选mentions
    - 具体来说，对于每个在test数据集中，并在启发式剪枝中留下来的mention mk，我们计算它的*mention coreference probability*，表示mk的“head noun”与其他mention产生共指关系的可能性。如果这个可能性没有超过阈值tc，我们就将mk从候选mention列表中移除。Section4将讲解tc如何结合共指关系成分参数来优化共指评价方法，的时候共同学习（这句话是不是语序有问题）
    - 我们从train data中计算mk的*mention 从reference probability*评估。具体来说，因为OntoNotes里仅有“无-单数”是被注释的。因此我们可以用mk的“head noun”被注释次数（在gold mentions），由mk的“head noun”所有的出现次数（分离）。
    - 如果mk的“head noun”没有在train data中出现，我们就设定它的“mcp”为1.意味着我们让它从过滤器中先pass掉。换句话说，我们比较保守，并且对于不能计算出“mcp”的mention不做处理。

#### Section 3. Coreference Resolution

- 概述
    - 像mention detection 组件中，我们的从reference resolution组件也采用了启发式和机器学习方法。
    - 我们使用了stanford的多轮共指消解方法（2011，Lee）来作为启发式共指消解。然而这些轮都是非词汇性的，我们用ML方法并结合词汇信息来增强多轮共指消解方法。
    - 尽管不同的轮是针对不同的语言使用的，但是我们吸收词汇信息后的方法每轮对于所有的语言是一样的（WTF？？？）
- The Multi-Pass Sieve Approach
    - 这轮由一个或者多个启发式规则组成。每个规则都基于一个或者多个条件，从两个mentions中提取一个共指关系。举个例子来说，一个在Standford的“discourse processing sieve”将按照以下规则判断两个mention是不是共指：
        1. 他们都是代词
        2. 他们都是同一个speaker说的（生产的/制造的）
    - sieves由他们的准确率进行排序。（？）
    - 为了确定一个文件中的mention集合，决策器对它们用了多轮（Multi-Pass）：
        - 在i-th pass中，仅用i-th中的规则对每个mention mk找一个先行词。当找这个先行词的时候，它的候选先行词被按一个顺序来访问，（这个顺序）通过它们在相关句法分析树的位置决定。
    - i-th中部分mentions的聚类，然后被传递（pass）给i+1-th pass。（人话，上次的聚类结果给下次用）
    - 因此，后面的passes可以充分利用前面的信息，但是之前确立的共指链不会比后面的更重要（？）
- The Sieves 
    - For English
        - 参照Standford的方法，采用12-sieves（Lee是13sieves，有一个是mention detection）
        - 因为我们加入了closed track，我们重复执行了10sieves，没有使用外部知识源。
        - 这10个sieves在Table2种list了。
        - 我们忽视了别名（Alias sieve）和词汇链（Lexical Chain sieve），这两个sieve用WordNet、WiKi和Freebase上的信息进行计算
    - For Chinese
        - 概述：
            - 我们参加了closed track 和open track
            - 这轮我们的应用对两个track都是相同的，除了我们对open track使用NE信息来改进某些系统。
            - 为了自动获取NE注释，我们使用了一个在train data中，通过gold NE注释训练出的**NE模型**
        - 中文决策器由**9轮**组成。(这里有个中英文对比的表格/Table2）
        - 这些sieves在基本上和英语参照相同的方式被执行，除了它们中的一小部分，（这一小部分）被修饰用以证明 一些独有的特性或者中文指代注释。（这句话有点儿难翻译）
        - 就像以下的详细介绍，（接下来会讲3个sieve）
            - 我们**介绍了一个新sieve**，the Chinese Head Match sieve；
            - **调整了两个现存的sieves**,the Precise Constructs sieve, the Pronoun sieve
        - **Chinese Head Match sieve**
            - 像Section2中说到的，一个mention和它的embedding mention能够称为共指关系是由于它们有相同头部。
            - 为了定位这些指代关系，我们执行了**Same Head sieve**，如果两个mention mj和mk有相同的Head并且mk is embedded within mj，（这个sieve）就假设两个mentions是共指的。
            - 这个规则有个**例外**，如果mj是一个由两个或者更多NP组成的同级（coordinate）NP，并且mk是这些NP之一，这两个mentions将不作为指代关系。
        - **Precise Constructs sieve**
            - 像Lee2011中的，Precise Construct sieve 判断两个mentions是不是共指关系的方法是基于信息，（这个信息）比如说一个mention是不是另一个mention的首字母缩略词，或者说它们是不是来自一个同位语关系或者系表关系。
            - 我们给这个sieve吸收其他的规则来处理中文缩写中特殊的例子。——外国人名的缩写、中国人名的缩写
        - **Pronouns sieves**
            - 这个sieve通过利用像mention的*性别、数量*这样的语法信息，解决了代词关系。
            - 这些语法信息主要针对英文，对于中文并不可信（not true）
            - 为了获取针对中文的像这样的语法信息，我们设计了一个简单的方法。如下三步：
                - 首先我们设定了简单的启发式来从这些中文NP中提取容易推断的语法信息。举例来说，我们可以启发式地确定性别，数量，物种，比如“ 她【she】是「Female，single，Animate」”；比如“ 它们【they】是「未知的，复数，无生命的」”。                再加上我们能决定一个有命名实体信息的mention的语法特征。举个例子，一个PERSON能够有指定的语法特性，「未知，单数，动物」
                - 其次，我们仿真了这些有启发式地已确定的语法特征值。观察在一个共指链中所有的mentions，它们的性别，数量，物种应该统一。详细来说，给定一个train文本，如果在共指链的一个mention是启发式的被语法信息所标记，我们自动所有的还需处理的mentions注释相同的语法特征值。
                - 最后，我们自动创建了六单词列表（six word lists），包含「1，物种词语；2，无生命词语；3，男性词语；4，女性词语；5，单数词；6，复数词」。
	                - Specifically,we populate these word lists with the grammatically annotated mentions from the previous step,where each element of a word list is composed of the head of a mention and a count indicating the number of time the mention is annotated with the corresponding grammatical attribute value.
                - 然后我们可以在test文本上用这些词链来确定mentions的属性值。由于这些词链规模较小，而且我们的目的是增加准确率。如果这三个属性中的每一个(?)，一个mention有一个未知(*Unknown*)属性而其他的mentions有已知(*Known*)属性，我们就将两个mentions考虑为共指关系。
        - 总结
            - 从Table2中可以看到，我们的中文系统没有*Relaxed String Match sieve*，不像英语有对应的。回顾这个sieve对两个mentions，如果跟在落下的文本的字符串紧跟着它们的head words是相同的，就把他们当作共指关系。（例子：*Michael Wolf*,and *Michael Wolf,a contributing editor for "New York".*)
            - 由于中文人名经常有单个字符组成，并且heads很少跟在别的中文词语后面，我们相信*Relaxed Head Match*对于确定中文的共指关系没什么用。
            - 因此，中文人名缩写这样的将会交给*Precise Constructs sieve*处理 
    - For Arabic
	    - 仅用了一轮，the exact match sieve。因为用别的（上面的）效果不好

- Incorporating Lexical Information(结合词法信息)
	- 像之前提到的一样，我们结合词法信息增强了这个sieve。
	- 为了利用词法信息，我们首先计算了*词法概率*。具体来说，对于文本中的每个mention mj和mk，我们首先计算两个概率：
		1. *string-pair（SP-Prob）*概率，也就是包含两个mentions的字符串sj和sk是共指的概率。
		2. *head-pair（HP-Prob）*概率，也就是两个mentions的head 名词hj和hk是共指的概率。
	- 为了更好的评价，我们对training data和这两个mentions进行预处理：
		1. 对每个英文单词进行小写转换
		2. 通过一个由	字符串形式对每个阿拉伯单词w进行替换，——**这句话是讲处理阿拉伯语的，看不懂，略**
	- 如果sj(hj)和sk(hk)没有在training数据集中出现的话，我们就将SP-Prob(mj,mk)(HP-Prob(mj,mk))标记为*Undefined*
	- 然后，我们通过对sieve方法提出两种扩展，然后用这些词法概率来增强mj和mk的处理结果。
		- 第一种扩展着力于增强sieve方法的*准确率*。具体来说，在进入任何sieve之前，我们需要确认SP-Prob(mj,mk)<=tSPL 或者HP-Prob(mj,mk)<=tHPL。如果是这样，我们的解析器将绕过所有的sieves，并且认为mj，mk不是共指的。
		我们用了词汇概率来增进准确度，具体来说通过假设两个mentions不是共指的，如果在training data中有“sufficient/足够的”信息来让我们做出这个决定。如果两个概率都没有定义，那么这个mentions对儿在过滤器中留存，然后给sieve管道做后续处理。
		- 第二种扩展着力于增强sieve方法的*召回率*。具体来说，我们创建了一个新的sieve，叫**”Lexical Pair sieve**，将这个sieve添加到sieve管道的最后面，如果SP-Prob(mj,mk)>=tSPU or HP-Prob(mj,mk)>=tHPU，就假设mj和mk是共指的。
		其他的类似第一种扩展，如果这两个概率都没有定义，那么这个sieve将不会处理这个mentions对儿。
		- 这四个阈值**tSPL，tHPL；tSPU，tHPU**，将在development 数据集上被优化

#### Section 4. Parameter Estimation（参数估计）
就像之前讨论的一样，我们在development数据上训练系统的参数来优化消解性能。我们的系统有两套可调节的参数。目前为止，我们先看一套参数，命名为*五词汇概率阈值*，包含tc、tSPL、tHPL、tSPU、tHPU。 再看第二套参数包含*rule relaxation parameters*.<p>
回顾一下，一个sieve中的每个规则都由一个或多个条件组成。我们联合条件 i 和参数 入i ，（这个参数）是一个控制条件i是否应该被去除的二值。特别的，如果 入i=0，条件i将被从相对应的规则中移除。

缓和参数的目的应当明确：他们允许我们用机器学习的方法去优化 hand-craft 规则。这一节提出了在development数据集上得到参数的的两种算法。

在讨论参数优化算法之前，先回顾一下简介。（简介是指）我们分辨特征的方法是我们建立了*genre-specific*分解器。换句话说，对每种语言的每个genre，我们

	1. 从相应的training数据中，学习词汇概率
	2. 获取最理想的参数值O1，O2，各自/依次用算参数估计算法1和2给development数据估计
	3. O1和O2之一，选择其中可以在development数据集上更好表现的一个来作为最后参数估计的set（？）

- 算法1
	- pass

- 算法2
	- pass

#### Section 5. Results and Discussion

完整的结果在table3中。

- mention detection results & coreference results 由准确率/召回率/F值来描述。
- 为了更好理解这两个参数sets的角色，我们展示了独立的实验。对每个语言-track
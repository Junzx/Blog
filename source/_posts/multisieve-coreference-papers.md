---
title: 基于多轮处理的指代消解系统-论文笔记
date: 2019-03-06
tags:
	- NLP
	- Coreference resolution
top: 1
description: 阅读Stanford两篇消解论文的笔记
---

### A Multi-pass sieve for coreference resolution

#### Abstract
- 其他的很多方法使用简单的决策来判定两个表述是否属于共指，由于低准确率的特征数往往高于高准确率的特征数，因此这将导致问题。
- 因此本文设计了一种模型，根据准确率的高低，由高到低堆叠了多个sieve，**每一sieve的输入是上一轮的实体类的输出**。此外，在一个实体类中还可以共享属性（性别、数量）。
- 这些sieve保证了高准确率的强特征起到更加有用的作用，保证了每一次的决策都使用了所有的信息（信息共享）
- 句法信息用于识别表述的中心词以及确定句子中表述的顺序
 
#### 获取候选表述

- 根据从左到右广度优先遍历句法树
- 

#### Sieves

1. Exact Match
> This model links two mentions only if they con-
tain exactly the same extent text, including modifiers and determiners, e.g., the Shahab 3 ground-ground missile. As expected, this model is extremely pre- cise, with a pairwise precision over 96%.

如果两个表述的修饰语和限定词相同，说明共指

2. Precise Constructs

如果以下条件被任意满足一个，那么两个表述共指

- Appositive-同位语
> the two nominal mentions are in an appositive construction, e.g., [Israel’s Deputy De- fense Minister], [Ephraim Sneh] , said . . . We use the same syntactic rules to detect appositions as Haghighi and Klein (2009).

两个**名词性表述**处在一个同位语结构中。我们参考了2009那篇论文的规则

- Predicate nominative-谓语主格
> the two mentions (nominal or pronominal) are in a copulative subject-object re- lation, e.g., [The New York-based College Board] is [a nonprofit organization that administers the SATs and promotes higher education] (Poon and Domin- gos, 2008).

两个表述（名词性/代词性）处在一个交错的主客体关系中。如：xxxx is xxx

- Role appositive-角色同位语
> the candidate antecedent is headed by a noun and appears as a modifier in an NP whose head is the current mention, e.g., [[ac- tress] Rebecca Schaeffer]. This feature is inspired by Haghighi and Klein (2009), who triggered it only if the mention is labeled as a person by the NER. We constrain this heuristic more in our work: we allow this feature to match only if: (a) the mention is labeled as a person, (b) the antecedent is animate (we detail animacy detection in Pass 7), and (c) the antecedent’s gender is not neutral.

如 [[演员]小明]。
要求：

    1. 表述被标记为PERSON
    2. 先行词是animate
    3. 先行词的性别不是中性

- Relative pronoun-关系代词-**没有实现**
> the mention is a relative pronoun that modifies the head of the antecedent NP, e.g., [the finance street [which] has already formed in the Waitan district].

这个表述是一个关系代词，它修饰了先行词的中心词

- Acronym-首字母缩略词
> both mentions are tagged as NNP and one of them is an acronym of the other, e.g., [Agence France Presse] . . . [AFP]. We use a simple acronym detection algorithm, which marks a mention as an acronym of another if its text equals the sequence of upper case characters in the other mention. We will adopt better solutions for acronym detection in future work (Schwartz, 2003).

- 两个表述都被标记为NNP
- 一个是另一个的缩写
- 论文里就用的**A**gence **F**rance **P**resse =  AFP

- Demonym-区域居民称谓词
> one of the mentions is a demonym of the other, e.g., [Israel] . . . [Israeli]. For demonym detection we use a static list of countries and their gentilic forms from Wikipedia.3

一个表述是另一个表述的～，比如 美国 = 美国人

3. Strict Head Matching

这个sieve的目的在于：简单的仅考虑中心词相同容易导致问题，比如【北京大学】和【清华大学】不是相同的

- Cluster head match
> the mention head word matches any head word in the antecedent cluster. Note that this feature is actually more relaxed than naive head matching between mention and an- tecedent candidate because it is satisfied when the mention’s head matches the head of any entity in the candidate’s cluster. We constrain this feature by en- forcing a conjunction with the features below.

这个表述的先行词匹配在候选集合中任意的中心词。

- Word inclusion

所有在表述类中的非停用词词语集合，包含在候选先行词的非停用词词语集合

- Compatible modifiers only-仅有兼容修饰语

表述的修饰语都包含在候选先行词的修饰语中，这个主要针对的是两个表述之间的关系，而不是两个cluster（上一个特征）

- not i-within-i
一个表述不能是另一个表述的孩子NP（child NP）

sieve3：

    - cluster head match
    - word inclusion
    - compatible modifiers only 
    - not i-within-i

4. 类似上一个sieve

    - cluster head match 
    - word inclusion
    - not i-within-i
    
5. 类似于上一个sieve
    - cluster head match
    - compatible modifiers only
    - not i-within-i

6. relaxed head matching

- 表述的中心词可以匹配任何候选先行词所在的cluster中的词语
- 要求表述和候选先行词被标记为同样的命名实体（同类）
- word inclusion
- not i-within-i


---
#### 设置共指的逻辑




---

### Stanford’s Multi-Pass Sieve Coreference Resolution System at the CoNLL-2011 Shared Task


1. **Mention Detection Sieve**
2. **Discourse Processing Sieve**
3. Exact String Match Sieve
4. **Relaxed String Match Sieve**
5. Precise Constructs Sieve (e.g., appositives)
6-8. Strict Head Matching Sieves A-C
9. **Proper Head Word Match Sieve**
10. **Alias Sieve**
11. Relaxed Head Matching Sieve
12. **Lexical Chain Sieve**
13. Pronouns Sieve
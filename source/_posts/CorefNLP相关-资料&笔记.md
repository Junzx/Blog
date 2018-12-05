---
title: CoreNLP资料
date: 2016-11-19 10:44:25
tags: 
	- CoreNLP
	- NLP
description: CoreNLP相关笔记
top: 1
---


- [一个日语关于CoreNLP的讲解](http://lab.astamuse.co.jp/entry/corenlp1)
- [coreNLP的使用](http://luchi007.iteye.com/blog/2285485)
- [Stanford CoreNLP 3.6.0 中文指代消解模块调用失败的解决方案](http://www.cnblogs.com/zklidd/p/5081677.html)
- [使用Stanford CoreNLP工具包处理中文](http://blog.csdn.net/jiangjingxuan/article/details/54906288)
- [深入迁出CoreNLP、可能暂无用](https://toutiao.io/posts/366808/app_preview)
- [Github上一个CoreNLP的demo](https://github.com/drewfarris/corenlp-examples/tree/master/src/main/java/drew/corenlp)
- [Github上搜索corenlp](https://github.com/search?utf8=%E2%9C%93&q=corenlp&type=)
- [Stanford Deterministic Coreference Resolution System](https://nlp.stanford.edu/software/dcoref.html)
- [CoreNLP主页](https://stanfordnlp.github.io/CoreNLP/coref.html#overview)
- [The Stanford CoreNLP Natural Language Processing Toolkit/ PDF](https://nlp.stanford.edu/pubs/StanfordCoreNlp2014.pdf)
- [**Coref文档**](https://nlp.stanford.edu/nlp/javadoc/javanlp/edu/stanford/nlp/)
- [Coref Github 代码](https://github.com/stanfordnlp/CoreNLP/tree/master/src/edu/stanford/nlp/coref)
- [从命令行使用斯坦福 CoreNLP](https://kkbac.wordpress.com/2016/11/25/%E4%BB%8E%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%BD%BF%E7%94%A8%E6%96%AF%E5%9D%A6%E7%A6%8F-corenlp/)
***
***
- 示范代码：
 来源：https://stanfordnlp.github.io/CoreNLP/coref.html#api

##### 输入：Barack Obama was born in Hawaii.  He is the president. Obama was elected in 2008.

##### 输出：
```
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator tokenize
[main] INFO edu.stanford.nlp.pipeline.TokenizerAnnotator - No tokenizer type provided. Defaulting to PTBTokenizer.
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator ssplit
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator pos
[main] INFO edu.stanford.nlp.tagger.maxent.MaxentTagger - Loading POS tagger from edu/stanford/nlp/models/pos-tagger/english-left3words/english-left3words-distsim.tagger ... done [0.9 sec].
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator lemma
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator ner
[main] INFO edu.stanford.nlp.ie.AbstractSequenceClassifier - Loading classifier from edu/stanford/nlp/models/ner/english.all.3class.distsim.crf.ser.gz ... done [1.4 sec].
[main] INFO edu.stanford.nlp.ie.AbstractSequenceClassifier - Loading classifier from edu/stanford/nlp/models/ner/english.muc.7class.distsim.crf.ser.gz ... done [1.7 sec].
[main] INFO edu.stanford.nlp.ie.AbstractSequenceClassifier - Loading classifier from edu/stanford/nlp/models/ner/english.conll.4class.distsim.crf.ser.gz ... done [0.5 sec].
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator parse
[main] INFO edu.stanford.nlp.parser.common.ParserGrammar - Loading parser from serialized file edu/stanford/nlp/models/lexparser/englishPCFG.ser.gz ... done [0.3 sec].
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator mention
[main] INFO edu.stanford.nlp.pipeline.MentionAnnotator - Using mention detector type: dependency
[main] INFO edu.stanford.nlp.pipeline.StanfordCoreNLP - Adding annotator coref
[main] INFO edu.stanford.nlp.coref.statistical.SimpleLinearClassifier - Loading coref model edu/stanford/nlp/models/coref/statistical/ranking_model.ser.gz ... done [1.2 sec].
---
coref chains
	CHAIN3-["Barack Obama" in sentence 1, "He" in sentence 2, "Obama" in sentence 3]
---
mentions
	Barack Obama
	Hawaii
---
mentions
	the president
	He
---
mentions
	Obama
	2008

```

##### 代码：

```
//这个文件是原版的示例代码，没有任何的改动
import java.util.Properties;

import edu.stanford.nlp.coref.CorefCoreAnnotations;
import edu.stanford.nlp.coref.data.CorefChain;
import edu.stanford.nlp.coref.data.Mention;
import edu.stanford.nlp.ling.CoreAnnotations;
import edu.stanford.nlp.pipeline.Annotation;
import edu.stanford.nlp.pipeline.StanfordCoreNLP;
import edu.stanford.nlp.util.CoreMap;

public class GoldCode {
	  public static void main(String[] args) throws Exception {
	    Annotation document = new Annotation("Barack Obama was born in Hawaii.  He is the president. Obama was elected in 2008.");
	    Properties props = new Properties();
	    props.setProperty("annotators", "tokenize,ssplit,pos,lemma,ner,parse,mention,coref");
	    StanfordCoreNLP pipeline = new StanfordCoreNLP(props);
	    pipeline.annotate(document);
	    System.out.println("---");
	    System.out.println("coref chains");
	    for (CorefChain cc : document.get(CorefCoreAnnotations.CorefChainAnnotation.class).values()) {
	      System.out.println("\t" + cc);
	    }
	    for (CoreMap sentence : document.get(CoreAnnotations.SentencesAnnotation.class)) {
	      System.out.println("---");
	      System.out.println("mentions");
	      for (Mention m : sentence.get(CorefCoreAnnotations.CorefMentionsAnnotation.class)) {
	        System.out.println("\t" + m);
       }
    }
  }
}


```


### 注：以上代码只针对英文句子有效，中文句子无法成功。


##### 需要调用的包：
![image](http://note.youdao.com/yws/public/resource/27feab63e93fe65035dae3a82b0a0cd5/xmlnote/C871BA8A94E24C14B56D3D5B3C998330/244)


---


```
import edu.stanford.nlp.coref.CorefCoreAnnotations;
import edu.stanford.nlp.coref.data.CorefChain;
import edu.stanford.nlp.coref.data.Mention;
import edu.stanford.nlp.ling.CoreAnnotations;
import edu.stanford.nlp.pipeline.Annotation;
import edu.stanford.nlp.pipeline.StanfordCoreNLP;
import edu.stanford.nlp.util.CoreMap;
```


This is not a problem of StanfordCoreNlpDemo program because I ran that code in Netbeans before. The problem seems associated with classpath issue.

Since the StanfordCoreNlpDemo.java file belongs to a package


```
package package edu.stanford.nlp.pipeline.demo;

public class StanfordCoreNlpDemo {
    public static final void main(String[] args) throws IOException {
        // code goes here
    } 
}
```

Then calling the following results in Error: Could not find or load main class TheClassName.

java -cp . StanfordCoreNlpDemo
It must be called with its fully-qualified name:

java -cp . edu.stanford.nlp.pipeline.demo.StanfordCoreNlpDemo
And this edu.stanford.nlp.pipeline.demo directory must exist in the classpath. In this example, ., meaning the current directory, is the entirety of classpath. Therefore this particular example must be called from the directory in which edu.stanford.nlp.pipeline.demo exists.

Reference

https://stackoverflow.com/a/29331827/5352399

https://stackoverflow.com/a/18093929/5352399

**StanfordCoreNLP的各个组件（annotator）按“tokenize（分词）, ssplit（断句）, pos（词性标注）, lemma（词元化）, ner（命名实体识别）, parse（语法分析）, dcoref（同义词分辨）”**
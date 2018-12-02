---
title: 爬虫初探——爬取百度贴吧
date: 2015-7-1
tags: 
    - 爬虫
    - 学习
description: 仿照他人的代码爬取百度贴吧的文本。
---


```
# -*- coding:utf-8 -*-
import re
import urllib2
class BDTB(object):
    def __init__(self,urlIn,seeLz):
        self.baseUrl=urlIn
        self.seeLz='?see_Lz='+str(seeLz)
    def getPage(self,page):
        try:
            self.baseUrl=self.baseUrl+self.seeLz+'&pn='+str(page)
            req=urllib2.Request(self.baseUrl)
            response=urllib2.urlopen(req)
            #return response.read().decode('utf-8')     # Maybe Bugs
            return response
        except Exception,e:
            print 'Open Error:',e
    def getTitle(self):
        try:
            aPage=self.getPage(1)
            pattern=re.compile(r'<h3 class="core_title_txt.*?" title="(.*?)" style.*?</h3>',re.S)
            result=re.search(pattern,str(aPage.read()))
            testWriteTool(result.group(1).strip())
            return result.group(1).strip()      # return a title of page
            #testWriteTool(aPage.read())
        except Exception,e:
            print 'Error in getTitle:',e
    def getPageNum(self):
        try:
            aPage=self.getPage(1)
            #pattern=re.compile(r'<li class="l_reply_num".*?<span class="red">.*?(\d*)</font>',re.S)
            pattern=re.compile(r'<li class="l_reply_num".*><span class.*>(\d+)</span>',re.S)
            #pattern = re.compile('<li class="l_reply_num.*?</span>.*?<span.*?>(.*?)</span>',re.S)
            result=re.search(pattern,str(aPage.read()))
            #print result.group(1).strip()
            return result.group(1).strip()
        except Exception,e:
            print 'Error in getPageNum:',e
    def getContent(self,page=1):
        try:
            i=1
            aPage=self.getPage(page)
            pattern=re.compile('<div id="post_content_.*?>(.*?)</div>',re.S)
            #pattern=re.compile('<div id="post_content_.*?>(.*?)</div>',re.S)
            items=re.findall(pattern,str(aPage.read()))
            #print 'we get ',len(items),'contents'
            f=open('ans.txt','a+')
            for item in items:
                temp=str(i)+':'+item.strip()+'\n'
                f.writelines(temp)
                i+=1
                #print item
            f.close()
        except Exception,e:
            print 'Error in getContent:',e
        else:
            print 'We Loading Txt....'
def testWriteTool(objStr):
    f=open('ans.txt','a+')
    f.writelines(objStr+'\n')
    f.close()
def startFunc(url):
    f=open('ans.txt','a+')
    f.truncate()
    f.close()
    #============= start clear file
    test=BDTB(url,1)
    if len(test.getPage(1).read())!=0:print 'yes we can conn'
    print 'Title:',test.getTitle()
    numOfPage=test.getPageNum()
    print 'PageNum:',numOfPage
    for i in range(1,int(numOfPage)+1):
        test.getContent(i)
if __name__ == '__main__':
    testUrl1='http://tieba.baidu.com/p/3138733512'      #2014-07-01 16:22
    testUrl2='http://tieba.baidu.com/p/3812772126'      #2015-06-07 20:53
    testUrl3='http://tieba.baidu.com/p/3180989704'      #2014-07-22 19:05
    
    #=======================
    #startFunc(testUrl1)
    startFunc(testUrl2)
    #startFunc(testUrl3)
```

参考：http://cuiqingcai.com/993.html
写的挺详细的 虽然在实现的时候也出了这样那样的错吧

## 运行时：

![image](/Baidu_tieba_spider/psb2.jpg)



## 运行结果：
![image](/Baidu_tieba_spider/psb.png)


---
title: ElasticSearch踩坑
date: 2019-12-28 21:49:51
tags:
  - ElasticSearch
description: 配置ElasticSearch时候踩的坑
top: 1
---

大概是官网：https://www.elastic.co/cn/downloads/elasticsearch


## 一些链接：

- MongoDB-Elasticsearch 实时数据导入：https://zhuanlan.zhihu.com/p/26906652
- 搭建ElasticSearch+MongoDB检索系统：https://www.cnblogs.com/jamespei/p/5694495.html
- Elasticsearch 权威指南（中文版）：https://es.xiaoleilu.com/ [elasticsearch-the-definitive-guide-cn.pdf](/uploads/25f3cdae1cd6b4b966c202c410e7e3ba/elasticsearch-the-definitive-guide-cn.pdf)


其他回答：

- elasticsearch（lucene）可以代替NoSQL（mongodb）吗？：https://www.zhihu.com/question/25535889
- 终于有人把Elasticsearch原理讲透了！：https://zhuanlan.zhihu.com/p/62892586
- ElasticSearch之排序使用-ES常用排序方法：https://blog.csdn.net/kjsoftware/article/details/76292911
- Elasticsearch系列六：ES中的倒排索引：https://lanffy.github.io/2019/05/10/Inverted-Index-In-Elasticsearch


## 安装

### Windows下安装

1. 去官网下载并解压缩
2. 双击执行 elasticsearch.bat，稍等片刻，打开浏览器，输入 http://localhost:9200 ，显式以下画面，说明ES安装成功：
![image](/ElasticSearch踩坑/1.png)
3. 安装head插件，此处有坑，见下一楼详情。
4. 安装kibana，参考：https://www.elastic.co/guide/cn/kibana/current/windows.html ，下载以后运行 `./bin/kibana.bat`，然后访问`http://localhost:5601/`


### Linux下安装

1. 官网(https://www.elastic.co/cn/downloads/past-releases#elasticsearch )下载并配置，参考楼下坑2
2. 使用docker安装，参考：https://www.cnblogs.com/jianxuanbing/p/9410800.html


## 坑

### 坑1： 安装head插件

进入bin目录执行：
> `plugin install mobz/elasticsearch-head`

此处可能报错为：

![image](/ElasticSearch踩坑/2.png)

需要执行：
> `elasticsearch-plugin install mobz/elasticsearch-head` 

但是也可能遇到这个错误：

![image](/ElasticSearch踩坑/3.png)

因此我们要通过以下操作来安装：
> `git clone https://github.com/mobz/elasticsearch-head.git`

进入该文件夹执行
> `npm install` # 这一步如果卡死了可以中断重新安一下

然后安装好了以后在此目录执行
> `npm start`

见到如下方式说明成功：

![image](/ElasticSearch踩坑/4.png)

在./config/elasticsearch.yml里面新增这句：
```
http.cors.enabled: true
http.cors.allow-origin: "*"
```

接下来修改head/Gruntfile.js，这个js文件在根目录下，Ctrl+F搜索connect关键词找到这个位置并新增红框的那句：

![image](/ElasticSearch踩坑/5.png)

然后重启npm以及elasticsearch，出现head出现以下说明成功：

![image](/ElasticSearch踩坑/6.png)

#### 参考:
- https://my.oschina.net/mengzhang6/blog/1632284
- https://blog.csdn.net/qq924862077/article/details/79994565
- https://www.twblogs.net/a/5b7d58662b71770a43deb838

#### 备注：

有链接要改`head/_site/app.js`，

```
编辑head/_site/app.js，修改head连接es的地址，将localhost修改为es的IP地址  
# 原配置  
this.base_uri = this.config.base_uri || this.prefs.get("app-base_uri") || "http://localhost:9200";  
# 将localhost修改为ES的IP地址  
this.base_uri = this.config.base_uri || this.prefs.get("app-base_uri") || "http://YOUR-ES-IP:9200";
```
实际上我修改以后并没有成功，所以我没有改这句


### 坑2-linux下配置安装-版本7.4.2

遇到以下问题：

![image](/ElasticSearch踩坑/7.png)

参考：https://blog.51cto.com/xpleaf/2327317


对于问题1，有以下解决方式：

- 临时修改：
 `ulimit -n 65536`
但是重新登录后就会恢复成默认值了。

- 永久修改
修改`/etc/security/limits.conf`配置，如下：

```
hadoop          soft    nofile  65536   # soft表示为超过这个值就会有warnning
hadoop          hadr    nofile  100000  # hard则表示不能超过这个值
```

对于问题2，有以下解决方式：

- 查看当前值
`sysctl vm.max_map_count`
- 临时设置
`sysctl -w vm.max_map_count=262144`
但是重启系统后就会失效。

- 永久性设置
修改配置文件`/etc/sysctl.conf`，如下：
```
vm.max_map_count=262144
```
需要重启后才生效。

对于问题3，有以下解决方式：

在安装目录下`elasticsearch-7.3.0\config\elasticsearch.yml`，将`cluster.initial_master_nodes: ["node-1"] `的注释放开，即可解决（实际没有解决）
（参考：http://longlonggo.com/post/436.html）

修改`discovery.seed_hosts: []`成服务器的IP，此错误解决，参考：https://discuss.elastic.co/t/problems-with-access-to-elasticsearch-form-outside-machine/172450/3

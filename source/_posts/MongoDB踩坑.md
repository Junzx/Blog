---
title: MongoDB踩坑
date: 2019-12-08 22:13:41
tags:
  - python
  - MongoDB
description: 学习MongoDB时候的笔记
top: 1
---

#### 安装MongoDB

1. windows
    1. 访问https://www.mongodb.com/download-center/community ，选择所需版本，我使用了Community版本，因为不用登录
    2. 安装刚刚下载的包，建议选择`custom`，然后在接下来的步骤中`安装MongoDB Compass`选项去掉，因为没有梯子可能会卡死，compass是一个可视化界面，可以后续通过https://www.mongodb.com/products/compass 下载安装
 
2. Linux服务器
  
    1. 去https://www.mongodb.org/dl/linux/x86_64 选择一个合适的版本wget到服务器（以我下载的mongodb-linux-x86_64-rhel62-v4.2-latest.tgz为例）
    2. 解压：`tar -xvzf mongodb-linux-x86_64-rhel62-v4.2-latest.tgz`，并将此文件夹改名为`MongoDB`
    3. 新建文件夹：data, log, conf，在data文件夹中新建一`db`文件夹
    4. 进入conf文件夹新建一`mongodb.conf`进行配置，![image](/MongoDB踩坑/1.png) 
    主要设置这几个参数，最后一个`fork`参数是指是否以后台运行


#### 启动MongoDB服务

1. Windows

    待补充，打开compass连接默认数据库就启动了，以后也会随电脑自启动

2. Linux服务器

    `./bin/mongod -f ./conf/mongodb.conf` 

    意思是使用bin文件夹中的`mongod`，并指定使用`mongodb.conf`配置文件进行运行，看到successfully即表示运行成功

    也可以通过命令行的方式：
        `mongod --dbpath d:/mongodb/data/data  --port 27137 --logpath d:/mongodb/logs --logappend `

#### 进入MongoDB后台

1. Windows

    请用compass

2. Linux服务器

    `./bin/mongo --port xxxx`

    此处有2坑。

       1. 这里执行的是bin文件夹的`mongo`与上一步的`mongod`差一个字母
       2. 如果没有使用默认的端口，此处进去后台需要指定*.conf中的端口，否则找不到

#### 基础MongoDB后台命令

- 创建数据库

    `use DATABASE_NAME` 如果数据库不存在，则创建数据库，否则切换到指定数据库。
- 查看所有数据库

    `show dbs` 注意，如果新创建了数据库但是没有插入数据，这里是不会显示的
- 查看某数据库下所有collection

    `show collections`
- 查看当前在哪个数据库上操作

    `db`
- 删除当前所在的数据库

    `db.dropDatabase()`
    
- 创建collection

    - 隐式创建：`db.my_coll.insert({'test':'11'})`
    - 显式创建：`db.creatCollection('my_coll)`

#### pymongo

```
# import
from pymongo import MongoClient 

# 连接库，注意需要启动服务并保证端口准确
client = MongoClient('mongodb://localhost:27017') 

# 选择其中一个数据库，如果没有则新建（类似于`use Material`）
db = client.Material 

# 获取所有collection名称
colls = db.list_collection_names()

# 选择其中一个集合，如果没有则新建（类似于`db.createCollection()`）
coll_act = db.articles 

# 插入数据——一次性插入多个
# ordered参数指示如果遇到异常是否继续，True为当场退出
# 有网友说一次只能插入1000条，但是我测试好像没有这个问题
coll_act.insert_many(lst, ordered=False) 

# 插入数据——一次插入一个
coll_act.insert_one({'test': 't'})

# 查找数据，返回的是cursor，可以使用np.array()或者pd.DataFrame()转
tmp = np.array(list(coll_act.find({}, {'vector': 1, '_id': 0}) # 1表示选择这个字段，无论如何都会返回_id，因此此字段置为0。注意，find里面有两个大括号
tmp = pd.DataFrame(list(coll_act.find())) # 这个很好使，注意先要转化为list

# 查找——select article, array FROM col WHERE _id=ObjectId("")
from bson.objectid import ObjectId
coll_act.find({'_id': ObjectId(file_id)},  {'article_id': 1, 'vector': 1})

# 关闭client
client.close()
```

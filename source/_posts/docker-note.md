---
title: Docker笔记
date: 2019-09-09 23:24:21
tags:
    - Docker
description: 配置docker时候的坑
top: 1
mathjax: False
---

#### 安装

1. 检查
Docker 要求 Ubuntu 系统的内核版本高于 3.10 ，使用`uname -r`

    ```
    > 4.15.0-50-generic
    ```

2. 安装 : `sudo apt-get install docker.io`

#### 镜像处理相关

1. 搜索镜像`docker search centos`
2. 拉取镜像`docker pull centos`
3. 查看镜像`docker images`
4. 创建镜像`sudo docker build /home/zz/GitlabCodes/consultant-nlp/similarity/similarity_docker/ -t similarity-docker-test`


#### 启动/重启服务

1. 启动服务`service docker start`
2. 重启服务`systemctl restart docker`


#### 操作容器

1. 创建/启动一个容器有如下两种方法
    1. 启动一个bash终端,允许用户进行交互：`docker run --name mydocker -it centos /bin/bash`
        ``` 
            # --name  给容器定义一个名称
            # -i  让容器的标准输入保持打开
            # -t 让Docker分配一个伪终端,并绑定到容器的标准输入上
            # /bin/bash 指定docker容器，用shell解释器交互
        ```
    2. 指定端口转发：`sudo docker run -itd -p 8080:8000 --name sim-docker-port centos`。注意，这个命令必须有"itd"的**d**，否则端口映射不过去

    3. 启动一个已有的容器`docker start e5f094e8d788`

2. 查看已有的容器：`sudo docker ps -a`，注：`docker ps`是显示当前运行的容器
    ```
    (base) zz@zz-VirtualBox:~/GitlabCodes/consultant-nlp/similarity/similarity_docker$ sudo docker ps -a
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                             PORTS               NAMES
    393e0a6addd4        centos              "/bin/bash"              40 seconds ago      Exited (0) 6 seconds ago                            frosty_robinson
    5087b7889418        centos              "/bin/bash"              2 minutes ago       Exited (0) About a minute ago                       sim-docker
    10cb8f4b5dff        nginx:latest        "nginx -g 'daemon of…"   34 minutes ago      Exited (0) 22 minutes ago                           myweb

    ```

3. 进入刚刚某个docker的命令行`sudo docker exec -it sim-docker /bin/bash`

4. 删除某个容器: `sudo docker rm sim-docker`；删除所有停止状态的容器`sudo docker container prune`

5. 打包某个容器`docker save`

6. 加载某个容器`docker load -i my.tar`


## 一个本地配置，上线服务器的配置流程

1. 安装docker`sudo apt-get install docker.io`
2. 拉取所需镜像`docker pull ubuntu`，搜索所需镜像使用：`docker search ubuntu`，注意OFFICIAL
3. 编写`Dockerfile`以及`requirement.txt`
4. 创建修改的镜像`sudo docker build /home/zz/GitlabCodes/consultant-nlp/similarity/similarity_docker/ -t similarity-docker`。这里similarity-docker是创建的镜像的名。
5. 打包`docker save -o similarity-docker.tar similarity-docker`，这里使用的是第四步创建的镜像。
6. copy到服务器
7. 解压/加载`docker load -i similarity-docker.tar`
8. 跑服务`sudo docker run -itd -p 8869:8869 --name sim-docker similarity-docker`
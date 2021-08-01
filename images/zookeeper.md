---
title: zookeeper
date: 2019-08-21 14:03:42
categories:
tags: util
---



#### 1. Zookeeper 作用

zookeeper可以用于命名、配置管理、服务注册与发现等。在分布式应用开发中，开发者可以使用zookeeper提供的高度抽象的API，完成应用间的协调与同步。

![zkservice](https://gitee.com/loick/image-url/raw/master/images/zookeeper/zkservice.jpg)

#### 2. Zookeeper 设计

##### 2.1 数据结构

我们首先来看一下zookeeper的数据机构，它非常像文件系统，由一个root节点 `/` 开始，可以在下面创建其他文件，与文件系统不同的是，这些文件夹本身可以存储数据，因此zookeeper官方用znode来表示这些节点。

zookeeper提供的抽象API就是对这些节点进行操作，一共是7个方法：

- create:：在指定位置创建节点
- delete：删除节点
- exists：检查节点是否存在
- get data：读取节点数据
- set data：写节点数据
- get children：获取子节点
- sync：同步其他节点的数据

![znode](https://gitee.com/loick/image-url/raw/master/images/zookeeper/zknamespace.jpg)

#### 使用

在有了上述API，我们就可以使用zookeeper构建分布式服务了。

假设我们分布式部署两个应用A和B，A服务依赖于B，为了确保服务A至少可以找到一个可用的B服务，我们可以使用zookeeper：

1. 创建zookeeper节点`/B `


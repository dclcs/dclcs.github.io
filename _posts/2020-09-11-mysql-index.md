---
title: 数据库索引
date: 2020-09-11 10：30
description: MySQL 索引

categories:
 - Database
tags: 
- Database
---


假设有一个表`T`，其初始化表语句如下：
```sql
mysql> create table T (
    ID int primary key,
    k int NOT NULL DEFAULT 0, 
    s varchar(16) NOT NULL DEFAULT '',
    index k(k))engine=InnoDB;
mysql> insert into T values(100,1, 'aa'),(200,2,'bb'),(300,3,'cc'),(500,5,'ee'),(600,6,'ff'),(700,7,'gg');
```

第一个问题:`select * from T where k between 3 and 5`，需要执行几次树搜索操作？


首先，看下这条SQL语句的执行流程：


- 在 k 索引树上找到 k=3 的记录，取得 ID = 300；
- 再到 ID 索引树查到 ID=300 对应的 R3；
- 在 k 索引树取下一个值 k=5，取得 ID=500；
- 再回到 ID 索引树查到 ID=500 对应的 R4；
- 在 k 索引树取下一个值 k=6，不满足条件，循环结束


在这个过程中，回到主键索引树搜索的过程，我们称为**回表**。可以看到，这个查询过程读了 k 索引树的 3 条记录（步骤 1、3 和 5），回表了两次（步骤 2 和 4）。

在这个例子中，由于查询结果所需要的数据只在主键索引上有，所以不得不回表。那么，有没有可能经过索引优化，避免回表过程呢？



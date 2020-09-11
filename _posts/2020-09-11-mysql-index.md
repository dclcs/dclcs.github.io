---
title: 数据库索引
date: 2020-09-11 10:30:50
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

### 覆盖索引

如果执行的语句是 `select ID from T where k between 3 and 5`，这时只需要查 ID 的值，而 ID 的值已经在 k 索引树上了，因此可以直接提供查询结果，不需要回表。也就是说，在这个查询里面，索引 k 已经“覆盖了”我们的查询需求，我们称为覆盖索引。


由于覆盖索引可以减少树的搜索次数，显著提升查询性能，所以使用覆盖索引是一个常用的性能优化手段。


### 最左前缀原则

B+ 树这种索引结构，可以利用索引的“最左前缀”，来定位记录。为了直观地说明这个概念，我们用（name，age）这个联合索引来分析。

![img](img/left_match.jpg)

当你的逻辑需求是查到所有名字是“张三”的人时，可以快速定位到 ID4，然后向后遍历得到所有需要的结果。

如果你要查的是所有名字第一个字是“张”的人，你的 SQL 语句的条件是 `where name like '张 %'`。这时，你也能够用上这个索引，查找到第一个符合条件的记录是 ID3，然后向后遍历，直到不满足条件为止。

可以看到，不只是索引的全部定义，只要满足最左前缀，就可以利用索引来加速检索。这个最左前缀可以是联合索引的最左 N 个字段，也可以是字符串索引的最左 M 个字符。

### 索引下推

Index Condition Pushdown，简称 ICP。 是Mysql 5.6版本引入的技术优化。旨在 在“仅能利用最左前缀索的场景”下（而不是能利用全部联合索引），对不在最左前缀索引中的其他联合索引字段加以利用——在遍历索引时，就用这些其他字段进行过滤(where条件里的匹配)。过滤会减少遍历索引查出的主键条数，从而减少回表次数，提示整体性能。 ------------------ 如果查询利用到了索引下推ICP技术，在Explain输出的Extra字段中会有“Using index condition”。即代表本次查询会利用到索引，且会利用到索引下推。 ------------------ 索引下推技术的实现——在遍历索引的那一步，由只传入可以利用到的字段值，改成了多传入下推字段值。
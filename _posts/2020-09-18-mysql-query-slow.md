---
title: 只查一行数据，也执行很慢的原因
date: 2020-09-18 22:10:50
description: Query a row, but slow

categories:
 - Database
tags: 
- Database
---


## 第一类 ： 查询长时间不返回

- 大概率是表锁住了，可以用`show processlist`来查看当前语句处于什么状态
- 等**MDL**锁
- 等`flush`
- 等行锁

## 第二类： 查询慢


## TODO : 复现

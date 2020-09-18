---
title: CPP CONCURRENCY IN ACTION
date: 2020-09-15 11:10:50
description: CPP THREAD

categories:
 - CPP
tags: 
- CPP
---

## 线程间共享数据

- 竞争条件(Race Condition)一般是有问题的竞争条件。
- 避免有问题的竞争条件
  - 无锁编程
  - 事务


## 用互斥元保护共享数据
- C++中的互斥元
  - `std::mutex`
  - `lock()`
  - `unlock()`
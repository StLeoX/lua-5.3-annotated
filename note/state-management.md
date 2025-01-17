# 状态管理

## 什么是状态

状态泛指：执行上下文、核心数据**等一切可存取的变量**。

---
划分：

1. 按照访问方式：这些变量可以划分为用户相关的（暴露给用户的）和内核维护的（对用户隐藏的）。用户相关的变量又可以划分可读、可读可写两类。
2. 按照声明周期（创建、销毁的时期）：这些变量可以划分为机器级别的和线程级别的。我们知道，Lua是单个线程在工作，所以线程的生命周期短于机器的，后者与进程是一致的。

## 状态的描述

机器状态的维护是通过`global_State`结构；线程状态的维护是通过`lua_State`结构。  
关联在于：`global_State`维护了一个活跃线程的列表，并通过`struct lua_State *twups`指向表头。
`lua_State`含有一个指向`global_State`的指针。  
两个结构所维护的数据是存在根本差异的。

lua_State的精妙
lua_State是一种封装了多方数据的复合结构，所以包含哪些字段基本就决定了VM的运行机制。




---
title: C 语言学习 (语法篇)
toc: false
categories:
  - 还没有分类
date: 2024-05-28 17:54:22
keywords:
description:
tags:
cover:
---

<!--
注释的方法：
在正文需要注释的地方插入下面的代码，根据需要修改编号：
  <sup>[1](#note1)</sup>
在"注"章节插入对应编号的注释内容:
  <div id="note1"></div>
  [1] 这是注的内容
-->

## 前言

## 简介

C 语言是一种广泛应用的编程语言，由美国贝尔实验室的 Dennis Ritchie 于 1972 年创立。这种语言的优势在于其跨平台的兼容性，可以在各种计算机系统上运行。C 语言能够直接操作硬件和内存，这使得它在处理底层任务时具有极高的效率。尽管 C 语言功能强大，但其语法规则相对简洁，易于掌握。C 语言在许多领域都有广泛的应用，包括操作系统、编译器、数据库、图形用户界面、嵌入式系统、网络通信和游戏开发等。

接下来开始 C 语言的学习。

<!-- more -->

## 变量与类型

变量是编程中的一个基本概念。

在计算机程序中，变量可以被视为存储数据的容器。每个变量都有一个特定的类型，决定了变量可以存储哪种类型的数据，例如整数、浮点数、字符或布尔值。

你不用先搞明白什么是整数、浮点数、字符或布尔值。

让我用一个更简单的比喻来解释什么是变量。

你可以把变量想象成一个储物箱。这个储物箱有一个标签，就像变量的名字。你可以把各种东西放进这个箱子里，比如数字、文字等。你也可以随时检查箱子里的东西，或者改变箱子里的东西。

*C 语言是一门静态类型语言。*

> [!tip]
> 静态类型语言是指变量的类型一旦声明就无法修改的编程语言。
> 如果暂时无法理解这个概念，暂时忽略它并不影响后续的学习。

这意味着 C 语言中任何变量都有一个明确的类型，并且该类型在编译时是可知的，并且在程序运行中不会发生变量类型的变化。当你在 C 语言中创建变量时，你必须在声明中给出该变量的类型。

> [!tip]
> 编译的概念后面会学到。

在这个示例中，我们初始化一个*整型变量 age*：

```c
int age;
```

这样我们就得到了一个变量。

在这里，`int`关键字(keyword)表示变量的类型是整型(intager)，`age`是变量名，`;`表示语句的结束。

在编程中，变量在声明的时候通常会赋予一个初始值。这样做有一些特殊的用意，会在之后章节中说明。

例如：

```c
int age = 0;
```

`=`是赋值运算符，用于给变量赋予值。

> [！tip]
> C 语言中还有其他的运算符，也同样会在后面的章节介绍。

变量也可以多次赋值，例如：

```c
int age = 0;
age = 10;
```

也可以使用变量给另一个变量赋值：

```c
int a = 10;
int b = a;
```

使用赋值运算符给变量赋值的时候，`=`右边的值或者变量的类型需要能够匹配左边的变量的类型。

> [!tip]
> 类型不匹配的时候会发生一些其他的事情。
> 在后面的章节我们将会学习到。

### 变量类型

C 语言的基本变量类型有*整型*、*浮点型*、*双精度浮点型*、*字符型*等。
完整的类型见下面表格。

| 类型 | 关键字 | 表示范围 |
| --- | --- | --- |
| 整数类型 | `int` | 通常为32位，表示整数范围：$$-2,147,483,648$$ 到 $$2,147,483,647$$ |
| 无符号整数类型 | `unsigned int` | 通常为32位，表示非负整数范围：$$0$$ 到 $$4,294,967,295$$ |
| 短整数类型 | `short` 或 `short int` | 通常为16位，表示整数范围：$$-32,768$$ 到 $$32,767$$ |
| 无符号短整数类型 | `unsigned short` 或 `unsigned short int` | 通常为16位，表示非负整数范围：$$0$$ 到 $$65,535$$ |
| 长整数类型 | `long` 或 `long int` | 通常为32位或64位，表示整数范围：$$-2,147,483,648$$ 到 $$2,147,483,647$$ 或 $$-9,223,372,036,854,775,808$$ 到 $$9,223,372,036,854,775,807$$ |
| 无符号长整数类型 | `unsigned long` 或 `unsigned long int` | 通常为32位或64位，表示非负整数范围：$$0$$ 到 $$4,294,967,295$$ 或 $$0$$ 到 $$18,446,744,073,709,551,615$$ |
| 字符类型 | `char` | 通常为8位，表示单个字符，例如字母、数字或符号 |
| 单精度浮点类型 | `float` | 通常为32位，表示浮点数范围：约 $$1.2 \times 10^{-38}$$ 到 $$3.4 \times 10^{38}$$ |
| 双精度浮点类型 | `double` | 通常为64位，表示浮点数范围：约 $$2.3 \times 10^{-308}$$ 到 $$1.7 \times 10^{308}$$ |
| 长双精度浮点类型 | `long double` | 通常为80位或128位，表示更高精度的浮点数 |

## 常量

## 运算符

## 条件语句

## 循环

## 数组

## 字符串

## 指针

## 函数

## 输入与输出

## 变量作用域

## 静态变量

## 全局变量

## 类型定义

## 枚举类型

## 结构体

## 命令行参数

## 头文件

## 预处理器

## 结语

## 注

无

## 参考

无
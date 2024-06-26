---
title: 【文档翻译】Lisp 的根源 - Lisp 编程语言的起源、进化与魅力
toc: true
categories:
  - 文档翻译
keywords:
  - Lisp
  - Lisp 之根
  - Lisp 的根源
  - The Roots of Lisp
  - 文档翻译
  - 程序语言与编程哲学
description: >-
  本文介绍了 Lisp 编程语言的起源、核心思想以及其发展历程。原文作者 Paul Graham
  向我们展现了Lisp如何通过简单的数据结构（列表）和基本函数来创造一种简洁而强大的编程语言。他还阐述了 Lisp
  的宏、闭包和动态作用域等特性。本文将帮助读者深入理解 Lisp 这门编程语言的本质和魅力。
tags:
  - Lisp
  - Lisp 之根
  - Lisp 的根源
  - The Roots of Lisp
  - 文档翻译
abbrlink: f47def09
date: 2023-03-13 13:54:28
cover:
---

《Lisp 的根源》是一个介绍 Lisp 编程语言的起源和核心思想的文章，由 Paul Graham 所著。Lisp 是由 John McCarthy 基于 λ 演算和递归函数的理论，用一种简单的数据结构——列表和几个核心函数创造出来的一门简洁且强大的编程语言。本文不仅展示了如何用 Lisp 实现其编译器和解释器，同时也说明了 Lisp 的一些重要特性如宏、闭包和动态作用域，目的在于让读者深入了解 Lisp 的本质和魅力。

![Lisp 漫画](%E3%80%90%E6%96%87%E6%A1%A3%E7%BF%BB%E8%AF%91%E3%80%91Lisp%20%E7%9A%84%E6%A0%B9%E6%BA%90/Lisp%E7%9A%84%E6%A0%B9%E6%BA%90.jpg)

<!-- more -->

## 前言

在 1960 年，John McCarthy 发表了一篇杰出的论文，他为编程做了类似于 [Euclid 为几何所做的事情 <sup>[1]</sup>](#note1)。他展示了如何通过一些简单的运算符和函数符号，构建一个完整的编程语言。他将这种语言称为 Lisp，即列表处理，因为他的一个关键思想是使用一种称为列表的简单数据结构来表示代码和数据。

了解 McCarthy 发现的内容是值得的，它不仅仅是作为计算机历史上的一个里程碑，而是作为我们现在编程趋势的一个模型。我认为到目前为止，已经有两个非常清晰、一致的编程模型：C 模型和 Lisp 模型。

这两种似乎是高地，中间是沼泽低地。随着计算机变得更强大，新开发的语言一直在向 Lisp 模型靠拢。过去 20 年中，一种流行的新编程语言的配方是：取 C 模型的计算方式，并逐渐加入从 Lisp 模型中取出的部分，如运行时类型和垃圾回收。

在这篇文章中，我将尽可能简单地解释麦卡锡发现了什么。目的不仅仅是了解 40 年前某人发现了一个有趣的理论结果，而且是要展示语言正在走向何方。Lisp 与众不同之处——事实上，Lisp 的定义特征——就是它可以用自身来编写。要理解麦卡锡这样说的意思，我们要重走他的步骤，把他的数学符号翻译成可以运行的 Common Lisp 代码。

## 七个原始操作符

一开始，我们定义一个表达式。一个表达式要么是一个原子，由一系列英文字母（例如 foo）组成；要么是一个由零个或多个表达式组成的列表，用空格分隔并用括号括起来。这是一些表达式：

```text
foo
()
(foo)
(foo bar)
(a b (c) d)
```

通过算数，表达式 **_1 + 1_** 得到值 **_2_**。合法的 Lisp 表达式也会得到值。如果一个表达式 **_e_** 产生一个值 **_v_** 我们说 **_e 返回 v_**。我们下一步定义有什么种类的表达式，以及每种类型返回什么值。

如果表达式是一个列表，我们称第一个元素为操作符，并且剩下的元素称为参数。我们接下来定义七个原始(某种意义上的公理)操作符：[**quote**](#quote)，[**atom**](#atom)，**eq**，**car**，**cdr**，**cons** 和 **cond**

### quote

(quote x) 返回 x。为了可读性，我们将 (quote x) 记为 'x

```repl
> (quote a)
a
> 'a
a
> (quote (a b c))
(a b c)
```

### atom

如果 x 是原子或空列表 ，(atom x) 返回元素 t 。其他情况返回 () 。在 Lisp 中我们按照管理使用原子 t 表示真，并且使用空列表表示假。

```repl
> (atom 'a)
t
> (atom '(a b c))
()
> (atom '())
t
```

既然我们现在有了一个参数被求值的操作，我们就可以展示 quote 的用途了。通过引用一个列表，我们可以保护它免于求值。当一个未引用的列表作为操作符（如 atom）的参数时，它会被当作代码来处理。

```repl
> (atom (atom 'a))
t
```

当一个列表被 quote 时，它会被当作一个普通的列表来处理。在这种情况下，它是一个包含两个元素的列表。

```repl
> (atom '(atom ）'a))
()
```

这对应于我们在英语中使用引号的方式。Cambridge 是马萨诸塞州的一个城镇，大约有 90,000 人。"Cambridge" 是一个包含九个字母的单词。

quote 可能看起来是有点陌生的概念，因为很少有其他语言有类似的东西。它与 Lisp 最独特的特征之一密不可分：代码和数据由相同的数据结构构成，quote 运算符是我们区分它们的方式。

### eq

如果 x 和 y 的值是相同的原子或都是空列表，则 (eq x y) 返回 t ，否则返回 () 。

**未完待续...**

## 注

<div id="note1"></div>
[1]《符号表达式的递归函数及其机器计算，第一部分》ACM 通讯 3:4，1960年4月，184-195页

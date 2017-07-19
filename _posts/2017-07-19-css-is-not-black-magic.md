---
layout: post
title:  "css不是黑魔法"
date:   2017-07-19 16:10:22 +0800
categories: css
published: true
origin: https://medium.freecodecamp.org/its-not-dark-magic-pulling-back-the-curtains-from-your-stylesheets-c8d677fa21b2
---
> 原文 :  [CSS Isn’t Black Magic]({{page.origin}})

#// TODO

作为一个前端开发者，你肯定会时不时的要和CSS打交道。
也许当你第一次接触到CSS的时候，感觉它很清爽，这里用CSS来加一个边框，哪里用CSS来改个颜色。
JavaScript才是前端最难的部分，不是吗？

随着前端水平的提高，这会发生改变。更糟的是很多前端开发者变得轻视CSS，认为他不过是一种玩具语言。但真实的情况是，当我们遇到困难的时候，许多开发者并不知道出问题的根本原因。

从我第一次参加培训起，我成为了一个全栈的js开发者，并且也或多或少的积累了一些CSS的知识。
作为JavaScript Jabber的小组成员，我也一直认为JS才是我的工作利器，我也因此花费了更多的精力在JS上。

从去年开始，我决定将精力集中在前端开发上，因此我发现我并不能像调试JS代码那样调试CSS样式。

我们都喜欢拿CSS来开玩笑，但是又有多少人真正的花些时间去理解我们所接触到的CSS代码呢。
又有多少人将我们遇到的CSS问题进行了进一步的抽象。
相反，我们仅仅采用了StackOverflow上最佳的答案或者是HACK，更甚至我们规避了整个问题。

对内部原理的理解可以帮助我们进行高阶的调试或者是性能调优。鉴于大部分开发者会议都是讨论常见的
CSS缺陷的修复，我的这篇文章主要将精力集中在进阶的浏览器的内部原理来帮助理解样式是如何被解析
和渲染的。

## DOM 和 CSSOM
首先，浏览器包含一个JS引擎和一个渲染引擎。我们现在只讨论渲染引擎。
我们会讨论一些基于Webkit、Blink、Gecko、Triden/Edge的特性。
浏览器会进行一系列的操作，包括**转换**、**划分词法单元**、**词法分析**、**语法解析**，
最后生成DOM和CSSOM


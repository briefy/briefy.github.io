---
layout: post
title:  "Unicode和javascript"
date:   2017-08-18 10:50:22 +0800
categories: trans js cn
published: true
origin: http://speakingjs.com/es5/ch24.html
---

  > 原文 :  [Unicode and JavaScript]({{page.origin}})

这篇文章将对Unicode做简要的介绍，并讲解JS是如何处理Unicode的。

## Unicode 的历史

Unicode的历史开始于1987年，
由 Joe Becker (Xerox), Lee Collins (Apple), and Mark Davis (Apple)发起，
目的是创造一种的统一的字符集，因为当时对于纯文本的编码有许多标准他们大多都不兼容，
比如，各种8字节ASCII编码的变体、大五码、GB2312编码等等。
在Unicode之前，也没有对于跨语言的纯文本编码的标准存在，但是却有许多富文本系统允许组合多种编码。

第一份Unicode草案提案发布于1988年，随着工作的进展工作组也扩大了。
Unicode 1.0 发布于1991年十月份，第二个版本发布于1992年七月份。

## Unicode中重要的概念

字符是一个简单的概念，但是相关的方面却有很多东西，因此Unicode是一个复杂的标准。
下面列出了一些基础但是重要的概念。

**字符和字素**（Characters and graphemes）

这两个术语表示东西有些相似，*字符*是数字实体，*字素*书写一种语言的最小单元。
程序员通常考虑的是字符，但是使用者通常考虑的是字素。
有时候好几个字符用来表示一个单个的字素。
比如，我们可以使用字符o和字符^来构造一个字素**ô**。

**标志符**（Glyph）

标志符是展示一个字素的一种具体的形式。有时候，根据上下文和其他一些因素的不同，
字素的展示也会不同。
比如下面的字符a

![image](/assets/img/a_small_glyphs.png)

**编码点**（code point）

Unicode用数来表示所支持的字符，这个数字就是**编码点**。
用十六进制来表示的话，编码点的范围是`0x0 ~ 0x10FFFF`。
也就是说Unicode的字符和编码点一一对应

**编码单元**（code units）

为了方便存储和转发编码点，编码点被编码成编码单元，一种固定长度的数据。
长度的单位是比特，不同的编码机制，长度不同，比如UTF-8和UTF-16。
如果编码点太大，超出了一个编码单元的范围，就会被分割成多个编码单元。
也就是说表示一个编码点的编码单元的数量可能不同。

编码单元，是具体的编码策略，比如，UTF-16、UTF-8的最小单位。

**字节序标志** （byte order mark）

如果编码单元大于一个字节的范围，就需要标明**字节序**。
字节序标志（BOM）是一个在文本开头的伪字符，用来标明编码单元是打断模式还是小端模式。
BOM也会标明使用的编码策略，比如UTF-8或者UTF-16等等。
此外，对于一段文本，如果浏览器没有显式的编码信息，默认从字节序标志里查找。

但是BOM并不会被经常使用，，
* UTF-8非常流行，他只有一种字节序，因此不需要BOM
* 有些编码已经标明了字节序，BOM就不再被使用了。比如，UTF-6BE、UTF-6LE、UTF-32BE、UTF-32LE。

**标准化** （Normalization）

鉴于字素可能有不同的表现形式，比如ô,即可以使用单一的编码点来表示，也可以是一个o和一个^。
标准化就是以一种规范化的格式来表示一个字素。

**字符属性** （character properties）

 每一个Unicode字符都被规范赋予了一些属性

 * **名称**（Name），英文名，由字母是、数字、-、空格组成。
   "λ"的名称是 "GREEK SMALL LETTER LAMBDA"
 * **通用分类**（General Category）， 比如， 字母、大写字母、数字、标点符号

 * **版本** （Age） 字符在哪个版本被加入Unicode
 * **废弃** （deprecated） 这个字符集是否被废弃不推荐使用了
 * 其他属性

 ## 编码点

 最初，编码点在Unicode的范围是16比特。
 从2.0版本的Unicode编码开始（07/1996），编码点的范围扩展到了21比特，
 被分割成17块，编号为0 - 16。

   * 块 0，    基本多语言编码块（BMP）， 0x0000 - 0xFFFF
   * 块 1，    补充多语言编码块（SMP）），0x10000–0x1FFFF
   * 块 2，    补充表意编码块（SIP），0x20000–0x2FFFF
   * 块 3-13， 未分配
   * 块 14，   补充特殊目的编码块（SSP）， 0xE0000–0xEFFFF
   * 块 15-16，补充私有使用区块（S PUA A/B）， 0x0F0000–0x10FFFF

Planes 1–16 are called supplementary planes or astral planes

## Unicode 编码方式

**UTF-32**  是一种使用32为编码单元的编码方式，这样一个编码点对应一个编码单元。
因此，UTF-32是唯一一种定长编码方式。对于其他编码方式来说，一个编码点对应的编码单元的数量是变化的。

**UTF-16** 是一种使用16为编码单元的编码方式，需要两个编码单元来表示一个编码点。
BMP块的编码点可以用一个编码单元来表示，其他的块的编码点需要两个编码单元来表示。

## Javascript源码和Unicode

js用两种方法来处理Unicode编码的源代码：
  * 内部， 解码阶段
  * 外部， 加载文件阶段

**源码内部解码**

js解析器将js源码看作是一系列UTF-16的编码单元。

比如，字符串、关键字、正则表达式，都可以用Unicode转移的序列来表示，\uHHHH。这里的HHHH是四个
十六进制的数字，比如，

```
  var f\u006F\u006F  = 'abc';
  foo
  //'abc'

  var λ = 123;
  \u03BB
  //123
```

这意味者，我们可以在字符串和变量名中使用Unicode字符，并且兼容ASCII编码范围的源码。

在字符串中，也支持十六进制字符转义序列，这种方式使用两位十六进制数字表示一个编码单元，
范围是0x00 - 0xFF.

```
  '\xF6' === 'ö'
  //true

  '\xF6' === '\u00F6'
  // true
```

**源码外部解码**

虽然js的内部解码用的是UTF-16，但是JS文件通常不用这种格式存储。当浏览器使用script加载js源码的时候，
使用下吗的策略来决定使用哪种编码方式解码：
  * 如果文件起始部分包含BOM，解码方式根据BOM的不同而不同
  * 否则，如果文件是通过HTTP（S）加载的话，根据 `Content-Type`中标明的编码方式解码，
  * 否则，根据script标签的charset属性决定
  * 最后使用html文件的编码方式解码。

## JS字符串和Unicode

**转义序列**

上面已经提到了，可以使用Unicode和十六进制两种转义序列。

```
 console.log('o\u0308');
 //ö
```

**统计字符数**

如果字符串中包含的编码点需要两个编码单元来表示的字符，那么， 这个时候 length返回的不在是字素的多少，
而是有多少编码单元。

```
 var str = '🐄';
 str ==== '\uD83D\uDc04'
 // true

 str.length
 // 2
```

在nodejs里，可以被修复，比如[punycode.js](https://github.com/bestiejs/punycode.js)。


```
 var puny = require('punycode');
 puny.ucs2.decode(str).length;
 // 1
```

**正则表达式和Unicode**

ES5的正则表达式对于unicode的支持是有限的。

行结束符会影响匹配，行结束符包含下面四种字符，

| 编码单元 | 字符名称           | 字符转义序列 |
| ------ | ------------------- | ------ |
| \u000A | Line feed           | \n     |
| \u000D | Carriage return     | \r     |
| \u2028 | Line separator      |        |
| \u2029 | Paragraph separator |        |


说明：

基于unicode定义的：

  * \s \S 是基于Unicode定义的
    ```
      /^\s$/.test('\uFEFF');
      // true
    ```
  * `.` 匹配所有的编码单元（**不是** 编码点）除了行结束符。
  * 多行模式 `\m`,`^` 匹配输入行的开始喝行结束后面的位置。`$`,匹配行结束符前面的位置和输入行的结尾。
    单行模式，只匹配输入的开始喝结尾。

下面的字符集，是基于ascii范围定义的不是unicode：

  * \d \D ,相当于[0-9]
  * \w \W ,相当于[a-zA-Z0-9_]
  * \b \B, 单词边界

    比如，在字符串'über'，\b这个字符的集合，认为字母b是单词的开始
    ```
      /\bb/.test('über');
      // true
    ```


**匹配任意的编码单元和任意的编码点**

匹配任意的编码单元，使用`[\s\S]`

匹配任意的编码点，`([\0-\uD7FF\uE000-\uFFFF]|[\uD800-\uDBFF][\uDC00-\uDFFF])`

## 参考资料

[Unicode.org](http://www.unicode.org/)

[Joel Spolsky’s introductory article “The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets (No Excuses!)”](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)

[“JavaScript’s internal character encoding: UCS-2 or UTF-16?” by Mathias Bynens](https://mathiasbynens.be/notes/javascript-encoding)

[“JavaScript, Regex, and Unicode” by Steven Levithan](http://blog.stevenlevithan.com/archives/javascript-regex-and-unicode)


## **TODO**

**TODO: 分析一下具体的编码策略，比如UTF-16，在计算机里是怎么存储的，怎么容错的。**

**TODO: study punnycode**

**TODO: 写一份punnycode的使用说明**

**leading surrogate 和 trailing surrogate**



---
layout: post
title:  "javascript,regex,Unicode"
date:   2017-08-19 13:10:22 +0800
categories: trans js regex cn
published: true
origin: http://blog.stevenlevithan.com/archives/javascript-regex-and-unicode
---

  > 原文 :  [javascript,regex,Unicodt]({{page.origin}})

并不是所有的转义字符集和js的正则表达式都能匹配Unicode字符。
有时候，确切的知道一个注意字符集匹配哪些东西很重要，这篇文章将会展开来讲一讲。

根据ES3的标准，`\s`、`\S`、`.`、`^`、`$`都是基于Unicode的，
 `\d`, `\D`, `\w`, `\W`, `\b`, 和 `\B`都是基于ASCII的。

看下面例子：
```
 /a\b/.test('naïve')
 // true
```

不同语言的正则表达式并不是都是相同的语法，虽然都是从perl演化过来的，但是**digit**、
**whitespace**、**word characotor**、**word boundary**和**newline**,
根据语言、字符集和操作系统的不同有不同的定义。

下面看一下javascipt中这些术语的意义。

* **Digit**         只表示0-9
* **whitespace**    Tab，line feed，vertical Tab，form feed，carriage return，
                space，no-break space， line separator， paragraph separator，
                and "any other Unicode 'space separator'"
* **word charactor** A-Z,a-z,0-9,_
* **word boundary**  The position between a word character and non-word character
* **newline**       The line feed, carriage return, line separator, and paragraph separator                         characters

(上面的符号不好翻译，感觉知道英文更重要，所以没有翻译)

下面是换行符以及他的Unicode编码

* `\u000a`  换行 \n
* `\u000d`  回车 \r
* `\u2028`  行分隔符
* `\u2029`  段落分隔符

CRLF(\r\n) 通常都是被当成独立的换行符
```
/\r^$\n/m.test("\r\n");
// true
```

`\u0009` — Tab — \t
`\u000a` — Line feed — \n — (newline character)
`\u000b` — Vertical tab — \v
`\u000c` — Form feed — \f
`\u000d` — Carriage return — \r — (newline character)
`\u0020` — Space
`\u00a0` — No-break space(可以使用js来指定这种space)
`\u1680` — Ogham space mark
`\u180e` — Mongolian vowel separator
`\u2000` — En quad
`\u2001` — Em quad
`\u2002` — En space
`\u2003` — Em space
`\u2004` — Three-per-em space
`\u2005` — Four-per-em space
`\u2006` — Six-per-em space
`\u2007` — Figure space
`\u2008` — Punctuation space
`\u2009` — Thin space
`\u200a` — Hair space
`\u2028` — Line separator — (newline character)
`\u2029` — Paragraph separator — (newline character)
`\u202f` — Narrow no-break space
`\u205f` — Medium mathematical space
`\u3000` — Ideographic space


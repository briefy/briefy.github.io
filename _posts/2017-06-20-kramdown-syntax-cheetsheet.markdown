---
layout: post
title:  "markdown cheet sheet"
date:   2017-06-20 09:02:22 +0800
categories: markdown kramdown syntax
---
### Paragrahps

1
==========
The first paragraph

Another paragraph

2
===
The first paragraph
Another paragraph

### Headers

first level header
==================

second level header
-----------------

# H1 header

# H2 header

### blockquotes

> A sample blockquote
>
> > Nested blockquotes are
> > alse possible
> ## Headers work too
> This is the outer quote again

### Code blocks

This is a sample code block.

    Continued here

~~~~~~
This is also a code block.
~~~
Ending lines must have at least as many tildes as the starting line.
~~~~~~~~

The following is a code block with a language specified:

~~~ javascript
function mycode(){
  return false;
}
~~~

### horizontal rules
* * *

---

### lists

1. This is a list item
2. And another item
3. and the third one

1. This is a list item
   > with a blockquote

   # And a header

2. Followed by another item


* item one
+ item two
- item three

### definition lists

term
: definition
: another definition

another term
and anther term
: and a definition for the term

### block attributes
> A nice blockquote
{: title="Blockquote title" .class1 .class2 #with-an-id}


### span level elements

*emphasized*

**strong**

__strong__


A [Link][kramdown ph]
to the home page

[kramdowm ph]: http://briefy@github.com

This is a text with a footnode[^1].

[^2]: And here is the definition.

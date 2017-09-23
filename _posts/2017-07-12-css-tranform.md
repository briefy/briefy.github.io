---
layout: post
title:  "css transform"
date:   2017-07-12 14:32:22 +0800ea
categories: css animation transform english
published: true
---

When we talk about animation, transformation is a big part of it.
We use `scale` to transform the size of the element, `translate` to make a move,
`rotate` to rotate,and so on.

However if we wanna be an expert about making animation,
we have to make it clear that the size about an element.
Actually, there are two kinds of sizes.

- document flow size, which has been decided by `width` and `height`;
- actual size, which will be decided by `scale`

So, i have to make it clear that when we use size values like `100px`,`100%` in transformation,it is about the `actual size`.

Here is an example, if we add the following style on an element

```css
   transform: scale(0.5,0.5) translate(700px);
```

you will not see a `700px` position translation,it will be `350px`,because we have been scaled down the element size to be half of the `document flow size`

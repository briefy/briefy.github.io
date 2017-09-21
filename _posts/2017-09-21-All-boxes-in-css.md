---
layout: post
title:  "All the boxes in css"
date:   2017-09-21 10:13:22 +0800
categories: box css en
published: true
---

## Containing Block

**Why is it important to identify the containing block?**
The size and position of an element are often impacted by its containing block. Percentage values that are applied to the `width`, `height`, `padding`, `margin`, and `offset` properties of an absolutely positioned element (i.e., which has its position set to `absolute` or `fixed`) are computed from the element's containing block

> if you need to find more details ,refer to this post.
> [All about the containing block](https://developer.mozilla.org/en-US/docs/Web/CSS/All_About_The_Containing_Block)

**what is the difference with BFC?**
BFC is just where you format you boxes;no relationship;

## terms
[Block-level elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)
[All about the containing block](https://developer.mozilla.org/en-US/docs/Web/CSS/All_About_The_Containing_Block)
[Understanding Block Formatting Contexts in CSS](https://www.sitepoint.com/understanding-block-formatting-contexts-in-css/)

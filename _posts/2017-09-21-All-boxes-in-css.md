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

**Relationships between 'display', 'position', and 'float'**

The three properties that affect box generation and layout — 'display', 'position', and 'float' — interact as follows:

1. If 'display' has the value 'none', then 'position' and 'float' do not apply. In this case, the element generates no box.
2. Otherwise, if 'position' has the value 'absolute' or 'fixed', the box is absolutely positioned, the computed value of 'float' is 'none', and display is set according to the table below. The position of the box will be determined by the 'top', 'right', 'bottom' and 'left' properties and the box's containing block.
3. Otherwise, if 'float' has a value other than 'none', the box is floated and 'display' is set according to the table below.
4. Otherwise, if the element is the root element, 'display' is set according to the table below, except that it is undefined in CSS 2.1 whether a specified value of 'list-item' becomes a computed value of 'block' or 'list-item'.
5. Otherwise, the remaining 'display' property values apply as specified

| specified value                          | computed value    |
| ---------------------------------------- | ----------------- |
| inline-table                             | table             |
| inline, table-row-group, table-column, table-column-group, table-header-group, table-footer-group, table-row, table-cell, table-caption, inline-block | block             |
| others                                   | same as specified |

## terms

- initial containing block
- containing block
- block formatting context
- inline formatting context
- block-level element
- inline-level element
- block container
- block boxes
- line-box


## resource

- [Block-level elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)
- [All about the containing block](https://developer.mozilla.org/en-US/docs/Web/CSS/All_About_The_Containing_Block)
- [Understanding Block Formatting Contexts in CSS](https://www.sitepoint.com/understanding-block-formatting-contexts-in-css/)

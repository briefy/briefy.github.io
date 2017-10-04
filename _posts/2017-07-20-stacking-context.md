---
layout: post
title:  "stacking context"
date:   2017-07-20 10:39:50 +0800ea
categories: stack-ctx css english
published: true
---

## Stacking only in the root context

When no element has a z-index, elements are stacked in this order (from bottom to top):

1. Background and borders of the root element
2. Descendant blocks in the normal flow, in order of appearance (in HTML)
3. Floating blocks
4. Inline descendants in the normal flow
5. Descendant positioned elements, in order of appearance (in HTML)

## Make a stacking context

A stacking context is formed, anywhere in the document, by any element in the following scenarios:

- Root element of document (HTML).
- Element with a `position` value `absolute` or `relative` and `z-index` value other than `auto`.
- Element with a `position` value `fixed` or `sticky` (sticky for all mobile browsers, but not older desktop).
- Element that is a child of a flex (`flexbox`) container, with `z-index` value other than `auto`.
- Element with a `opacity` value **less than** 1 (See the specification for opacity).
- Element with a `mix-blend-mode` value **other than** `normal`.
- Element with any of the following properties with value **other than** `none`:
  - transform
  - filter
  - perspective
  - clip-path
  - mask / mask-image / mask-border
- Element with a `isolation` value `isolate`.
- Element with a `-webkit-overflow-scrolling` value `touch`.
- Element with a `will-change` value specifying any property that would create a stacking context on non-initial value (see this post).

## related CSS properties

**z-index**
**isolation**
**mix-blend-mode**
**background-blend-mode**

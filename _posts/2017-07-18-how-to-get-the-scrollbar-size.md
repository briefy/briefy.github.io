---
layout: post
title:  "how to get the scrollbar size"
date:   2017-07-18 18:11:50 +0800ea
categories: solution js english
published: true
---
This post will use a example to demonstrate the geometry of DOM elements and put down of small snippet of `how to get the scrollbar size`.

## TODO: use d3 to graph the geometry data below


snippet of get the scrollbar size
```ts
function getScrollBarSize() {
    let size = 0;
    const inner = document.createElement('div');
    inner.style.width = '100%';
    inner.style.height = '200px';

    const outer = document.createElement('div');
    const outerStyle = outer.style;

    outerStyle.position = 'absolute';
    outerStyle.top = 0;
    outerStyle.left = 0;
    outerStyle.pointerEvents = 'none';
    outerStyle.visibility = 'hidden';
    outerStyle.width = '200px';
    outerStyle.height = '150px';
    outerStyle.overflow = 'hidden';

    outer.appendChild(inner);

    document.body.appendChild(outer);

    const widthContained = inner.offsetWidth;
    outer.style.overflow = 'scroll';
    let widthScroll = inner.offsetWidth;

    if (widthContained === widthScroll) {
      widthScroll = outer.clientWidth;
    }

    document.body.removeChild(outer);

    size = widthContained - widthScroll;
  return size;
}
```

### Open the console to examine the log result of DOM geometry.
dimentions are

```
  client offset scroll
  width  height top left
```

 <iframe src="/assets/geometry.html" style="width:500px;height:500px;" />
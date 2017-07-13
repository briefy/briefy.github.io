---
layout: post
title:  "css transform-origin"
date:   2017-07-13 09:50:50 +0800ea
categories: css animation transform-origin english
published: true
---

`transform-origin`, it is a point relative to which we do the transformation.

usage syntaxt:

```css
transform-origin: x-axis y-axis z-axis|initial|inherit;
```

default value:

```css
50% 50% 0 /* percent is about the non-scaled size,so as to say dom-flow size */
```



About was the basic usage, and we have to notice that `transform-origin`
can be animated, so we can take advantage of `transform-origin` to indicate
the trend of a movement direction of an element.

example below:
> if we use `scale(1,1)`, we can not see the movement.

```html
<!doctype html>
<html>
  <head>
    <title>
      transform-origin
    </title>
    <style>
       .anim{
         animation-name: anim;
         animation-fill-mode: both;
         animation-duration: 8s;
         animation-iteration-count: infinite;
       }
       @keyframes anim{
         0% {
           transform-origin: 0% 0%;
           transform: scale(0.5,0.5);
         }

         25% {
           transform-origin: 0% 100%;
           transform: scale(0.5,0.5);
         } 
         50% {
           transform-origin: 50% 50%;
           transform: scale(0.5,0.5);
         }
         75%{
           transform-origin: 100% 0%;
           transform: scale(0.5,0.5);
         }

        100%{
          transform-origin: 0% 0%;
          transform: scale(0.5,0.5);
        }

       }
      </style>
  </head>
  <body>
    <div class="anim" style="width: 100px;height: 100px;background:red;">
        transform-origin
    </div>
  </body>
</html>
```

---
layout: post
title:  "quiks in javascript"
date:   2017-08-21 10:13:22 +0800
categories: js english
published: true
---

## isNaN and Number.isNaN

`isNaN` global has a quirk,
It returns `true` if its argument is NaN,
or if that argument is **a non-numeric value** such as a string or an object.

However, Number.isNaN only return `true`,
when the argument is `NaN`.

```
  isNaN(NaN)  === true;
  isNaN({})   === true;
  Number.isNaN({}) === false;
```

**polyfill**
```
  (function(global){
    var isNaN = global.isNaN;

    Object.defineProperty(Number,'isNaN',{
      value: function(value){
        return typeof value === 'number' && isNaN(value);
      }
      configurable: true,
      enumerable: false,
      writable: true
    });
  })(this)
```


## coercion

Let see the table below, these are  the implicit coersions.


![image](/assets/img/coersion-table-js.png)

we can get something strange:

```
  [] == 0
  "" == 0
  false == 0
```

how to do the explicit coersion

```
Number("3")   // => 3
String(false) // => "false" Or use false.toString()
Boolean([])   // => true
Object(3)     // => new Number(3)

x + "" // Same as String(x)
+x     // Same as Number(x). You may also see x-0
!!x    // Same as Boolean(x). Note double !

// Same as parseInt
~~1.4
~~'briefy'
1.4>>>0
'briefy'>>0
```



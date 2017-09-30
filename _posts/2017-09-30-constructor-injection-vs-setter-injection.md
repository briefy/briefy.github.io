---
layout: post
title:  "构造器注入和setter注入"
date:   2017-09-30 10:13:22 +0800
categories:  design-pattern trans chinese
published: true
origin: http://misko.hevery.com/2009/02/19/constructor-injection-vs-setter-injection/
---
# 构造器注入和setter注入

  > 原文 :  [Constructor Injection vs. Setter Injection]({{page.origin}})

关于依赖注入目前有两大阵营

- 构造器依赖注入
- setter依赖注入

从依赖注入的历史来看，setter注入来自于使用spring的阵营，构造器注入来自于
使用pic－container和GUICE的阵营。我们先把这些历史因素放在一边，来对比一
下这两种策略的不同。

## Setter注入

setter注入指的是利用*无参*的构造器和合理的默认值来创建对象。
对象的用户可以调用不同的setter方法来覆盖默认的依赖，从而实现依赖注入。

## 构造器注入

构造起注入是指创建对象的时候没有默认依赖，实例化对象之前利用构造器方法
来传入依赖的对象

乍一看，setter注入似乎更好，构造函数没有参数，无论是在生产环境还是测试
环境创建对象都非常简单。不过，构造器注入有一个不是很明显的有点，让我觉得
构造器注入更好用。构造器注入增强了对象初始化阶段的顺序并且避免了循环依赖。
使用setter注入，对象实例化依赖注入的顺序并不明确，并不知道什么时候需要
的依赖全部注入了。典型的应用当中也许会有非常多的依赖者，这些依赖的注入都需要setter。
构造器依赖注入会自动的在构造函数中明确依赖的顺序并且完成相应的对象的实例化。
并且，当最后一个对象实例化完成之后，依赖注入的阶段就完成了。

我们来看一个实例化`CreditCardProcessor`的例子

``` java
  CreditCardProcessor processor
    = new CreditCardProcessor();
```

很好，我们已经实例化了`CreditCardProcessor`,但这就够了吗？
不够，我们需要知道去掉用`setOfflineQueue()`，不过这个信息并不是很明显。

```java
  OfflineQueue queue = new OfflineQueue();
  CreditCardProcessor processor
    = new CreditCardProcessor();
  processor.setOfflineQueue(queue);
```

好的，我们已经实例化了`OfflineQueue`并且记得将`queue`作为依赖注入到了`processor`，可是，结束了吗?
没有，你需要给`queue`和`processor`分别设置数据库。

```java
  Database db = new Database();
  OfflineQueue queue = new OfflineQueue();
  queue.setDatabase(db);
  CreditCardProcessor processor
          = new CreditCardProcessor();
  processor.setOfflineQueue(queue);
  processor.setDatabase(db);
```

等一下，这就结束了吗？你还需要设置数据库的`Username`、`password`和`URL`。

```java
  Database db = new Database();
  db.setUsername("username");
  db.setPassword("password");
  db.setUrl("jdbc:....");
  OfflineQueue queue = new OfflineQueue();
  queue.setDatabase(db);
  CreditCardProcessor processor
          = new CreditCardProcessor();
  processor.setOfflineQueue(queue);
  processor.setDatabase(db);
```

现在终于结束了吧？我觉得可以了，但是我怎么确定呢？我知道可以利用框架
来解决这个问题，但是如果我使用的语言没有这种框架呢？

现在我们来看看使用构造器注入是如此的简单。

我们来实例化`CreditCardPrecossor`。

```java
CreditCardProcessor processor
        = new CreditCardProcessor(?queue?, ?db?);
```

我们还没有结束，我们需要一个`queue`和一个`database`。

```java
  Database db = new Database(
          "username", "password", "jdbc:....");
  OfflineQueue queue = new OfflineQueue(db);
  CreditCardProcessor processor
          = new CreditCardProcessor(queue, db);
```

每一个构造器方法的参数都考虑到了，我们的工作结束了，并不需要框架的介入。
而且，如果构造器的参数不合法的化，我们的代码甚至通不过编译，我们根本不会遇到
实例化依赖顺序错误的问题。

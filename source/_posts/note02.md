---
title: defaultValue 与 Value 的使用
---

问题起因：某天boss在例行检查代码的时候，把所有的value换成了defaultValue，原因是他说value的值是从props过来的，props的值改变会影响value，而defaultValue可以避免这个问题....（黑人问号脸.jpg)，啊这不是吧，源数据改变就算换成defaultValue也会改变的吧，难道是我一直理解错了？于是本着辨证的目的我打算互联网冲浪去寻找原因...

<!--more-->

在查阅了一些资料文献后我发现了这样一段话可以解答我的疑惑

> **React 中为何需要defaultValue？**
>
> defaultValue 一般用于表单，给表单元素一个初始化值。注意，只是初始化，如果defaultValue值发生变化，表单里的值不会被改变。
>
> **value也可以做到，为何还要defaultValue呢？**
>
> 表单分两种，一种是受控表单，一种是非受控表单。仅用value，使用者会误以为value值改变，表单显示的值也会跟着变，这实际上是受控表单的行为，完全符合期望。但是，非受控表单，props.value变化，其表单显示的值不会跟着变（因为表单内部有自己的state），为了区别这两种场景，所以引入了defaultValue，表示只给默认值。

果然是基础知识不扎实，看到这儿，我大概理解了boss为什么将原来的value onChange搭配改为了defaultValue onBlur；原来的搭配会在键入的时候频繁的执行setState去更改数值，改为非受控组件后，并在失去焦点的时候赋值，避免了大数据列表因为不断更改值应发的性能问题，真真儿nice
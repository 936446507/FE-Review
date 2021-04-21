# 对症下药—— DOM 优化原理与基本实践



## DOM 为什么这么慢

![img](https://user-gold-cdn.xitu.io/2018/9/29/166254bce949ca58?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

JS 引擎和渲染引擎（浏览器内核）是独立实现的。当我们用 JS 去操作 DOM 时，本质上是 JS 引擎和渲染引擎之间进行了“跨界交流”

我们对 DOM 的操作都不会局限于访问，而是为了修改它。当我们对 DOM 的修改会引发它外观（样式）上的改变时，就会触发**回流**或**重绘**。

- 回流：当我们对 DOM 的修改引发了 DOM 几何尺寸的变化（比如修改元素的宽、高或隐藏元素等）时，浏览器需要重新计算元素的几何属性（其他元素的几何属性和位置也会因此受到影响），然后再将计算的结果绘制出来。这个过程就是回流（也叫重排）。
- 重绘：当我们对 DOM 的修改导致了样式的变化、却并未影响其几何属性（比如修改了颜色或背景色）时，浏览器不需重新计算元素的几何属性、直接为该元素绘制新的样式（跳过了上图所示的回流环节）。这个过程叫做重绘。



### 减少 DOM 操作，使用DocumentFragment，文档片段

**DocumentFragment，文档片段**接口，一个没有父对象的最小文档对象。它被作为一个轻量版的 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 使用，就像标准的document一样，存储由节点（nodes）组成的文档结构。与document相比，最大的区别是DocumentFragment 不是真实 DOM 树的一部分，它的变化不会触发 DOM 树的[重新渲染](https://developer.mozilla.org/zh-CN/docs/Glossary/Reflow)，且不会导致性能等问题。
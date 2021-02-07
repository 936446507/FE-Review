# 本地存储——从 Cookie 到 Web Storage、IndexedDB



## Cookie

### Cookie的性能劣势

- #### Cookie 不够大

- #### 过量的 Cookie 会带来巨大的性能浪费

  **Cookie 是紧跟域名的，同一个域名下的所有请求，都会携带 Cookie**



## Web Storage

Web Storage 是 HTML5 专门为浏览器存储而提供的数据存储机制。它又分为 Local Storage 与 Session Storage。

### Local Storage 与 Session Storage 的区别

两者的区别在于**生命周期**与**作用域**的不同。

- 生命周期：Local Storage 是持久化的本地存储，存储在其中的数据是永远不会过期的，使其消失的唯一办法是手动删除；而 Session Storage 是临时性的本地存储，它是会话级别的存储，当会话结束（页面被关闭）时，存储内容也随之被释放。
- 作用域：Local Storage、Session Storage 和 Cookie 都遵循同源策略。但 Session Storage 特别的一点在于，即便是相同域名下的两个页面，只要它们**不在同一个浏览器窗口中**打开，那么它们的 Session Storage 内容便无法共享。

### Web Storage 的特性

- 存储容量大： Web Storage 根据浏览器的不同，存储容量可以达到 5-10M 之间。
- 仅位于浏览器端，不与服务端发生通信。



## IndexedDB

### IndexedDB 的应用场景

通过上面的示例大家可以看出，在 IndexedDB 中，我们可以创建多个数据库，一个数据库中创建多张表，一张表中存储多条数据——这足以 hold 住复杂的结构性数据。IndexedDB 可以看做是 LocalStorage 的一个升级，当数据的复杂度和规模上升到了 LocalStorage 无法解决的程度，我们毫无疑问可以请出 IndexedDB 来帮忙。
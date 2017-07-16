# 前端架构篇

##### Vue 1 和 Vue 2 的区别

**如果你没有用过 Vue 1，不要强答！**  
Vue 2 与 Vue 1 最大的区别，是 Vue 2 引入了 Virtual-DOM，提升了对 DOM 操作的效率。  
同时，Vue 2 提供了更严格单向数据流形式。Vue 2 完全取消了双向绑定，子组件不能直接修改父组件传入的任何数据（这一点我觉得是参考借鉴了 React）。在 Vue 2 中，子组件只能通过触发事件的形式通知父组件修改数据，再反馈给子组件更新视图。  
事件传递部分，Vue 2 取消了 `dispatch` 和 `broadcast` 。Vue 2 的所有自定义组件默认不冒泡，只能在组件自身上使用 `emit` 触发。为了解决这个问题，Vue 2 引入了 Event Bus 的概念，通过一个额外的 Vue 实例来管理跨组件事件（JavaScript 中的观察者模式）。  
关于 Vue 1 和 Vue 2 更详细的区别，我写过一篇文章：[http://www.jianshu.com/p/90b995c113fc](http://www.jianshu.com/p/90b995c113fc)

##### 前后端分离的优点和缺点

这道题我的思路不是很清晰，

###### 优点

前后端分离后，前后端研发人员可以更专注于自己负责的部分，而不需要总是同时兼顾前端和后端。传统的后端整合前端的方式，开发调试都非常麻烦，分离之后的开发效率会更高。

###### 缺点

前后端分离后，数据过分的依赖 Ajax 和 RPC 等进行传递，性能相对低下。

##### 前端工程化的意义

##### 什么是 MVC，什么是 MVP，什么是 MVVM

可以参考阮一峰老师的一篇文章：[http://www.ruanyifeng.com/blog/2015/02/mvcmvp\_mvvm.html](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)

###### MVC

![](/assets/mvc.png)
View：用户界面
Controller：业务逻辑
模型：数据存储
在这种模式中，通信关系一般是这样的：
1. 用户通过 View 将指令传送到 Controller，或直接通知 Controller（比如直接改变URL）。
2. Controller 完成业务逻辑后，通知 Model 改变状态。
3. Model 层将新的状态反馈到 View 上，用户得到反馈。

###### MVP

![](/assets/mvp.png)
MVP 将 Controller 替换成了 Presenter 。
View 和 Model 全部通过 Presenter 相互联系，也就是说，Presenter 是整个模式的核心。
View 不部署任何业务逻辑，称为“被动视图（Passive View）”，而 Presenter 非常厚，包含所有业务逻辑。

###### MVVM

![](/assets/mvvm.png)
MVVM 将 Presenter 替换成了 ViewModel 。它与 MVP 的区别在于，View 与 ViewModel 是双向绑定的，View 的变动会自动反映在 ViewModel 上，反之亦然。

##### Vuex 的实现原理
https://tech.meituan.com/vuex-code-analysis.html

##### 项目如何模块化

谈谈个人的理解：
1. 对项目结构进行模块划分。
2. 选用模块化的架构，比如 React 和 Vue 。
3. 对项目目录进行模块化划分，将相似的组件或功能进行归类。举一个简单的 Vue 的例子：

```
- components
    - ComponentA.vue
    - ComponentB
        - Header.vue
        - Footer.vue
- views
    - index.vue
    - list.vue
- utils
    - axios.vue
- store
    - index.js
    - mutation-types.js
    - actions.js
    - modules
        - cart.js
```

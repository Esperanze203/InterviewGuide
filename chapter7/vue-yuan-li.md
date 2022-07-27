# Vue 原理

### 1 vue原理-大厂必考

为什么考察原理？

1.知其然知其所以然\
2.了解原理，才能应用的更好（竞争激烈，择优录取）\
3.大厂造轮子（有钱有资源，业务定制，技术KPI）

如何考察vue原理？

1.考察重点，而不是考察细节。掌握好2/原则。\
2.考察和日常使用相关联的原理，例如vdom、模板渲染\
3.整体流程是否全面？热门技术是否有深度？

Vue原理包括：

<mark style="color:red;">组件化</mark>\ <mark style="color:red;">响应式</mark>\ <mark style="color:red;">vdom和diff</mark>\ <mark style="color:red;">模板编译</mark>\ <mark style="color:red;">渲染过程</mark>\ <mark style="color:red;">前端路由</mark>

### 2 如何理解MVVM

#### 组件化基础

1.‘很久以前’就有组件化\
2.数据驱动视图（MVVM,setState）

'很久以前'的组件化：\
1.asp  jsp php已经有组件化了\
2.nodejs中也有类似的组件化数据驱动视图：\
&#x20;   1.传统组件，只是静态渲染，更新还要依赖于操作DOM；\
&#x20;   2.数据驱动视图-Vue MVVM；\
&#x20;   3.数据驱动视图-React setState（暂时按不下看）组件化是之前就有的，Vue和React搬过来，做了一个创新：**数据驱动视图**。

#### Vue MVVM

![](http://cdn.processon.com/5e88c5efe4b0bf3ebcf871af?e=1586025472\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:vxNlixoROv7FD\_gxeS5y4L967ug=)

M:Model\
V:View\
VM:ViewModel

View是视图，就是DOM；\
Model是模型，就是vue组件里的data，或者说是vuex里的数据；\
这两者通过ViewModel这一层来做关联，像监听事件，监听指令；\
通过这一层，在Model修改的时候，就能立即执行到View的渲染，\
View这层有什么点击事件，各种DOM事件监听的时候，都可以修改Model的数据。

### 3 监听data变化的核心API是什么

Vue响应式组件

data的数据一旦变化，立刻触发视图的更新\
实现数据驱动视图的第一步\
考察Vue原理的第一题

核心API-Object.defineProperty\
如何实现响应式，如何监听对象（深度监听），监听数组，代码演示\
Object.defineProperty的一些缺点（Vue3.0启用Proxy）

Proxy有兼容性问题

Proxy兼容性不好，且无法polyfill\
Vue2.x还会存在一段时间，所以都得学

Object.defineProperty

基本用法

![](http://cdn.processon.com/5e89541ae4b09396a49f6a6d?e=1586061866\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:EKHAYLr1fIxerSxn-ccbQ24wfRA=)

实现响应式

1.监听对象，监听数组\
2.复杂对象，深度监听\
3.几个缺点

### 4 如何深度监听data变化

代码演示

observe.js

![](http://cdn.processon.com/5e8960a3e4b0bf3ebcf8d11b?e=1586065075\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:3WB\_o7pTjgeW-hSvmXY1BYtbF\_U=)

function defineReactive

![](http://cdn.processon.com/5e895db4e4b0a1e6dcb3ece9?e=1586064325\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:vAuMZlkJH\_1c1TRSvkKqE6D6k8A=)

function observer

![](http://cdn.processon.com/5e895ddde4b03231c716703b?e=1586064365\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:sd1x0UhyKsUl0dJwTd63Nbaqe40=)

Object.defineProperty

**缺点**

1.深度监听，需要递归到底，一次性计算量大\
2.无法监听新增属性/删除属性（可以用Vue.set   Vue.delete解决）\
3.无法原生监听数组，需要特殊处理

### 5 vue如何监听数组变化

代码演示

扩展4.4中的observe.js

![](http://cdn.processon.com/5e89a88ce4b03404567ea2c8?e=1586083484\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:wK1FbKP3gMkRpDF3l5xqKIB7tOA=)

重新定义数组原型

![](http://cdn.processon.com/5e89a8c8e4b0bf3ebcf95aea?e=1586083545\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:2uugihCZewKrc4BJfENPgiGOW6A=)

Object.create（）\
创建新对象，原型指向 oldArrayProperty ，\
再扩展新的方法不会影响原型

![](http://cdn.processon.com/5e8962dce4b0bf3ebcf8d447?e=1586065644\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:RSPOSuDVVmlRfuKMuEKzkxo\_xfk=)

### 6 虚拟DOM-面试里的网红

虚拟DOM(Virtual DOM)和diff

1.vdom是实现vue和react的重要基石\
2.diff算法是vdom中最核心、最关键的部分\
3.vdom是一个热门话题，也是面试中的热门问题1.DOM操作非常耗费性能\
2.以前jQuery,可以自行控制DOM操作的时机，手动调整\
3.Vue和React是数据驱动视图，如何有效控制DOM操作？

解决方案—vdom

1.有了一定的复杂度，想减少计算次数比较难\
2.能不能减少计算，更多的转移为JS计算？因为JS执行速度很快\
3.vdom -用JS模拟DOM结构，计算出最小的变更，操作DOM

用JS模拟DOM结构

JS模拟DOM结构

![](http://cdn.processon.com/5e89aca3e4b03231c7170611?e=1586084531\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:cPNmCVU2UO7LphR8fTFA0hPUC8Q=)

1\. tag ，标签\
2\. props，属性(包括 id 、className 、style、事件等)\
3\. childrens，子元素，数组或者字符串

通过snabbdom学习vdom

1.简洁强大的vdom库，易学易用\
2.Vue参考它实现的vdom和diff\
3\. https://github.com/snabbdom/snabbdom\
1.Vue3.0重写了vdom的代码。优化了性能\
2.但vdom的基本理念不变，面试考点也不变\
3.React vdom具体实现和Vue也不同，但不妨碍统一学习

### 7 用过虚拟DOM吗

snabbdom

代码演示

![](http://cdn.processon.com/5e89f701e4b0a1e6dcb5059f?e=1586103570\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:csODr6hyIxqjKxNCMYGXiY1sHIw=)

snabbdom中代码的解析：\
h是一个函数，接收三个参数（标签或选择器，属性，子节点数组），返回的是一个vnode结构；\
patch(container,vnode) //把vnode渲染到空的DOM结构中\
patch(vnode,newVnode) //更新已有的内容\
patch(container,null) //清空DOM结构

snabbdom重点总结：\
h函数\
vnode数据结构\
patch函数

vdom总结：\
用JS模拟DOM结构（vnode）\
新旧vnode对比，得出最小的更新范围，最后更新DOM\
数据驱动视图的模式下，有效控制DOM操作

### 8 虚拟DOM-diff算法概述

diff算法：\
diff算法是vdom中最核心、最关键的部分\
diff算法能在日常使用vue React中体现出来（如key）\
diff算法是前端热门话题，面试“宠儿”

diff算法概述\
diff即对比，是一个广泛的概念，如linux diff命令、git diff等\
两个js对象也可以做diff，如https://github.com/cujojs/jiff\
两棵树做diff，如这里的vdom diff

树diff的时间复杂度O(n^3)\
第一，遍历tree1；第二，遍历tree2\
第三，排序\
1000个节点，要计算1亿次，算法不可用

优化时间复杂度到O(n)\
只比较同一层级，不跨级比较\
tag不相同，则直接删掉重建，不再深度比较\
tag和key，两者都相同，则认为是相同节点，不再深度比较

图示同层比较

![](http://cdn.processon.com/5e89fafbe4b0a1e6dcb50b7c?e=1586104588\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:VnJch2T\_jzjk8j6PRI7jrYd6e7o=)

tag不同，则直接删掉重建，不再深度比较

![](http://cdn.processon.com/5e89fb1fe4b09396a4a09843?e=1586104623\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:5Y8yZACTBnMKFdjiOYSYWVujgZk=)

### 9 深入diff算法源码-生成vnode

看源码的时候，\
找到核心函数，h()  patch()等\
看它的参数、返回值和主要逻辑\
不要过于抠细枝末

### 10 深入diff算法源码-patch函数

### 11 深入diff算法源码-patchVnode函数

### 12 深入diff算法源码-updateChildren函数

### 13 虚拟DOM-考点总结和复习

diff算法总结

1.patchVnode\
2.addVnodes  removeVnodes\
3.updateChildren(key的重要性)

vdom和diff 总结

1.细节不重要，updateChildren的过程也不重要，不要深究\
2.vdom核心概念很重要：h、vnode、patch、diff、key等\
3.vdom存在的价值更加重要：数据驱动视图，控制DOM操作

### 14 模板编译前置知识点-with语法

模板编译

1.模板是vue开发中最常用的部分，即与使用相关联的原理\
2.它不是html，有指令、插值、JS表达式，到底是什么？\
3.面试不会直接问，但会通过“组件渲染和更新过程”考察1.前置知识：JS的with语法\
2.vue template compiler将木模板编译为render函数\
3.执行render函数生成vnode

with语法改变{}内自由变量的查找规则，当做obj属性来查找\
如果找不到匹配的obj属性，就会报错\
with要慎用，它打破了作用域规则，易读性变差

![](http://cdn.processon.com/5e8ad02de4b09396a4a1658d?e=1586159165\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:A83p5YbuGAUAwZYBKIx8z\_Ur1ac=)

### 15 vue模板被编译成什么

模板编译

理解vue模板并不是html，而是要转换成可执行的js代码，也就是render函数。\
编译过程中生成的函数都是render函数（with这些），返回值是vnode，然后渲染。![](http://cdn.processon.com/5e8b1689e4b064d902d3512f?e=1586177177\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:05bnethiVIi9PoHHM3TeURwl2f0=)

模板编译为render函数，执行render函数返回vnode；\
基于vnode再执行patch和diff；\
使用webpack vue-loader，会在开发环境下编译模板（重要）\
使用vue-cli是集成webpack环境的，编译模板的工作都是在打包的时候做的，也就是产出的代码就没有模板了，全是render函数的形式了。这也算是vue性能优化的一点，这也是一种共识。\
但是如果只是自己创建的简单的vue项目（html+js），没有集成webpack环境，它是在浏览器运行时才编译的。

### 16 vue组件可用render代替template

vue组件中使用render代替template

![](http://cdn.processon.com/5e8b18c9e4b03bfcd0827e33?e=1586177753\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:gXEdrek8UFJAnDYvHO070N5x8aw=)

在有些复杂情况中，不能用template，可以考虑用render\
React一直都用render（没有模板），和这里一样

总结：

with语法\
模板到render函数，再到vnode，再到渲染和更新\
vue组件可以用render代替template

### 17 回顾和复习已学的知识点

响应式、模板编译、vdom是vue原理的三个核心知识点

1\. **响应式**：监听data属性 getter setter（包括数组）\
核心的API：\
Object.defineProperty（target, key, {\
&#x20;   get(){}, set(newValue){}\
}）\
&#x20;1）重新定义数组原型\
&#x20;2）深度监听对象\
2\. **模板编译**：模板到render函数，再到vnode\
3\. **vdom**：patch(elem, vnode)和patch(vnode, newVnode)

组件 渲染/更新 过程

初次渲染过程\
更新过程\
异步渲染

### 18 vue组件是如何渲染和更新的

初次渲染过程：\
解析模板为render函数（或在开发环境已完成，vue-loader）\
触发响应式，监听data属性 getter setter (模板中用到的变量会触发getter)\
执行render函数，生成vnode，patch(elem, vnode)

执行render函数会触发getter\
注意：如果模板中没有用到的data数据就不会触发getter，因为和视图没关系![](http://cdn.processon.com/5e8b2eb3e4b09396a4a24763?e=1586183363\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:QddlOmZZO9nHn2SH-A16uGAvSfs=)

更新过程：\
修改data，触发setter（此前在getter中已被监听）\
重新执行render函数，生成newVnode\
patch(vnode, newVnode)

流程图![](http://cdn.processon.com/5e8b2f13e4b09396a4a24842?e=1586183459\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:EuDh\_0VAffSjv6Fd9Cfk\_MTzKtA=)

### 19 vue组件是异步渲染的

异步渲染回顾$nextTick\
汇总data的修改，一次性更新视图\
减少DOM操作次数，提高性能

![](http://cdn.processon.com/5e8b306ee4b034045680e33e?e=1586183806\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:PgoUC28mq4q7Z9cqHeUjl\_qrqi0=)

### 20 如何用JS实现hash路由

前端路由原理：\
稍微复杂一点的SPA（single page app 单页面应用），都需要路由\
vue-router也是vue全家桶的标配之一\
属于"和日常使用相关联的原理"，面试常考

vue-router的路由模式：\
hash\
H5 history

url

![](http://cdn.processon.com/5e8b330ae4b034045680e8f1?e=1586184474\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:-gvAw6m7EqsiwO9TM9Tw1kF9Roo=)

**网页url组成部分**\
protocol-协议\
hostname-主机名,可能是ip地址或域名 host-主机名+端口\
port-端口\
pathname-url的路径\
search-?号之后的参数\
hash-#之后的部分

hash

hash特点

hash变化会触发网页跳转，即浏览器的前进、后退\
hash变化不会刷新页面，SPA必需的特点\
hash永远不会提交到server端（前端自生自灭）通过hash的变化来触发路由的变化，hash的跳转触发路由的跳转，hash的后退触发路由的后退。\
这就是通过hash的方式来触发路由，来触发视图的渲染。

hash变化

![](http://cdn.processon.com/5e8b342ce4b07e41dc2edeba?e=1586184764\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:CsGPOmwm6Xyo\_fUEbrt-fYUdxsc=)

1\. JS修改url // location.href = "#/user"\
2\. 手动修改url的hash //在浏览器地址栏手动修改hash，但是注意如果修改了url的其它部分可能会触发页面刷新，而且会触发前进后退\
3\. 浏览器前进、后退 //在浏览器操作前进后退，会导致hash变化

### 21 如何用JS实现H5 history路由

H5 history：\
用url规范的路由，但跳转时不刷新页面\
history.pushState\
window.onpopstate

![](http://cdn.processon.com/5e8b3cade4b0bf3ebcfbbede?e=1586186942\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:NISEcFMoK1axYogeFDZj2sLMZ5c=)![](http://cdn.processon.com/5e8b3c8ce4b03bfcd082d3d2?e=1586186908\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:hte79H1MYyBT795CFvJaTY52lwI=)

![](http://cdn.processon.com/5e8b3de0e4b09396a4a26c5b?e=1586187249\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:6-Y1ZOm6fUxSPsXLXyLpJz47zu4=)

const state = { name: 'page1' }\
history.pushState( state, '', 'page1' ) //重要！\
window.onpopstate = (event) => { //重要！\
event.state //通过pushState设置的state，在浏览器前进后退的过程中，只要页面跳转到page1，state就会带出来，也就是设置的state就对应了page1这个路由\
}

H5 history的模式需要后端的配合，\
参考vue官方文档无论你访问什么样的路由，最终返回的都是index.html这个路由\
如果没有做后端配置的兼容性，当访问到page1这个路由，点击刷新，就会报错page1页面找不到；\
所以后端做兼容性处理，无论访问哪个路由，都是index.html页面，然后再由前端通过history.pushState()的方式除触发路由的切换；\
也就是所有路由的切换都由前端来做，后端只需要返回index.html的主文件。

总结：

1.hash-window.onhashchange\
2.H5 history-history.pushState和window.onpopstate\
3.H5 history需要后端支持

两者选择

1\. toB的系统推荐使用hash，简单易用，对url规范不敏感\
2\. toC的系统，可以考虑选择H5 history,但需要服务端支持\
3\. 能选择简单的，就别用复杂的，要考虑成本和收益

### 22 vue原理-考点总结和复习

#### Vue 原理-总结

1.组件化\
2.响应式\
3.vdom和diff\
4.模板编译\
5.渲染过程\
6.前端路由

#### 1 组件化

1.组件化的历史\
2.数据驱动视图\
3.MVVM

#### 2 响应式

1\. Object.defineProperty\
2.监听对象（深度），监听数组\
3.Object.defineProperty的缺点（Vue3用Proxy，后面讲）

#### 3 vdom和diff

1.应用背景(重要)\
2.vnode结构（重要）\
3.snabbdom

#### 4 模板编译

1.with语法\
2.模板编译成render函数\
3.执行render函数生成vnode

#### 5 组件渲染/更新过程

1.初次渲染过程\
2.更新过程\
3.异步渲染

#### 6 前端路由原理

1.hash\
2.H5 history\
3.两者对比 如何选择\

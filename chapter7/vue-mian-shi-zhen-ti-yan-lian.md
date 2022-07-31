# Vue 面试真题演练

### 1.v-show和v-if的区别

1\. v-show  通过CSS display控制显示和隐藏\
2\. v-if  组件真正的渲染和销毁，而不是显示和隐藏\
3\. 频繁切换显示状态用v-show，否则用v-if

### 2. 为何在v-for中用key

1\. 必须用key，而不能是index和random\
2\. diff算法中通过tag和key来判断，是否是sameNode\
3\. 减少渲染次数，提升渲染性能

### 3. 描述Vue组件的生命周期（父子组件）

1\. 单组件生命周期图\
2\. 父子组件生命周期关系

### 4. Vue组件如何通讯（常见）

1\. 父子组件  props和this.$emit\
2\. 自定义事件event.$on   event.$off  event.$emit\
3\. vuex

### 5. 描述组件渲染和更新的过程

![](http://cdn.processon.com/5e8b48c3e4b064d902d3c335?e=1586190035\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:FZXCJlkeWXzInUmQFvgmjzTlpiM=)

三大部分响应式![](http://cdn.processon.com/5e8b4916e4b064d902d3c3c2?e=1586190118\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:Ltol9AKi6XMWBPm98OmhDq3ch6g=)

模板渲染![](http://cdn.processon.com/5e8b490be4b09396a4a2819a?e=1586190107\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:LjeSTRTJwLmuM68Yi-eVZ0gZq5k=)

虚拟dom![](http://cdn.processon.com/5e8b4923e4b03231c71980d3?e=1586190131\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:ClUjnO2uL1hm-k4e\_Fv7bi84M7c=)

### 6.双向数据绑定v-model的实现原理

1\. input元素的  value=this.name\
2\. 绑定input事件 this.name=$event.target.value\
3\. data更新会触发re-render

### 7. 对MVVM的理解

![](http://cdn.processon.com/5e8b4a3ce4b064d902d3c5a9?e=1586190412\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:nwg9jnW2dSIKx-CMeAuQhOp\_P28=)

### 8. computed有何特点

1\. 缓存，data不变不会重新计算\
2\. 提高性能

### 9. 为何组件data必须是一个函数？

![](http://cdn.processon.com/5e8b4ac7e4b09396a4a28476?e=1586190551\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:YVCHbqS77Eq6Pl0q55LmkEXxOqQ=)

vue组件的export default看似是一个对象，实际上在编译之后vue是一个class类，在不同地方多处使用这个vue组件时，相当于是对这个类的实例化。实例化时去执行data，如果data不是函数，那多处实例化的这个组件的data数据都会是一样了，改变一个data变量，也会影响其它实例化了这个组件的这个变量。但是如果data是函数，data中的数据就会在闭包中，不会相互影响。\
所以data必须是一个函数。

### 10. ajax请求应该放在哪个生命周期？

1\. mounted（组件已经渲染完，DOM加载完）\
2\. JS是单线程的，ajax异步获取数据\
3\. 放在mounted之前没有用，只会让逻辑更加混乱\
（在mounted之前，js没有渲染完，数据也是异步获取过程中，不会有提前的效果）

### 11. 如何将组件所有props传递给子组件？

1\. $props\
2\. \<User v-bind='$props'/>\
3\. 细节知识点，优先级不高

### 12. 如何自己实现v-model

![](http://cdn.processon.com/5e8b4ca0e4b064d902d3c975?e=1586191025\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:6VdrOF8NNbLMtHqGwP90ANjtfnU=)

### 13. 多个组件有相同的逻辑，如何抽离？

1\. mixin\
2\. 以及mixin的一些缺点

### 14. 何时使用异步组件？

1\. 加载大组件\
2\. 路由异步加载

### 15. 何时使用keep-alive?

1\. 缓存组件，不需要重复渲染\
2\. 多个静态tab页的切换\
3\. 优化性能

### 16. 何时需要使用beforeDestory

1\. 解绑自定义事件event.$off\
2\. 清楚定时器\
3\. 解绑自定义DOM事件，如window scroll等防止内存泄露

### 17. 什么是作用域插槽

![](http://cdn.processon.com/5e8b4eb5e4b0bf3ebcfbdf48?e=1586191557\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:cNrdaSWaEk\_dPGfOGEd4Y23Gysc=)

### 18. Vuex中action和，mutation有何区别

1\. action中处理异步，mutation不可以\
2\. mutation做原子操作\
3\. action可以整合多个mutation

### 19. Vue-router常用的路由模式

1\. hash默认\
2\. H5 history(需要服务端支持)\
3\. 两者比较

### 20. 如何配置Vue-router异步加载

![](http://cdn.processon.com/5e8b4faee4b09396a4a28bc0?e=1586191807\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:ZkrnzuDKr1geuF9uwErQVj4acEg=)

* （）=>import()

### 21. 用vnode描述一个DOM结构

![](http://cdn.processon.com/5e8b502fe4b07e41dc2f16bf?e=1586191935\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:yDg5Bdog4K-uiytCP73VmsIAZlc=)

### 22. 监听data变化的核心API是什么

1\. Object.defineProperty\
2\. 以及对象深度监听、监听数组\
3\. 有何缺点

### 23. Vue如何监听数组变化

1\. Object.defineProperty不能监听数组变化\
2\. 重新定义原型，重写push pop等方法，实现监听\
3\. Proxy可以原生支持监听数组变化

### 24. 请描述响应式原理

1\. 监听data变化\
2\. 组件渲染和更新流程

### 25. diff算法的时间复杂度

1\. O（n）\
2\. 在O(n^3)基础上做了一些调整\
同一层级比较。。。。

### 26. 简述diff算法过程

1\.  patch(elem,vnode)和patch(vnode,newVnode)\
2\. patchVnode和addVnodes和remoVnodes\
3\. updateChildren（key的重要性）

### 27. Vue为何是异步渲染，$nextTick何用？

1\. 异步渲染（以及合并data修改）以提高渲染性能\
2\. $nextTick在DOM更新完之后，触发回调

### 28. **Vue**常见**性能优化**方式

1. 合理使用v-show和v-if
2. 合理使用computed
3. v-for时加key，以及避免和v-if同时使用
4. 自定义事件、DOM事件及时销毁
5. 合理使用异步组件
6. 合理使用keep-alive
7. data层级不要太深
8. 使用vue-loader在开发环境做模板编译（预编译）
9. **webpack层面的优化**（后面讲）
10. **前端通用的性能优化**，如图片懒加载
11. 使用SSR
    * v-for和v-if同时使用时，由于v-for的优先级更高，每次都要计算v-if，造成性能浪费。
    * 响应式监听，深度监听需要一次性遍历完成。data层级太深时，递归的次数多。\

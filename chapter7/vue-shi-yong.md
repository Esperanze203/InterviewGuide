# Vue使用

### 1 vue使用-考点串讲

### 2 vue基本使用

#### 基本使用

1.日常使用，必须掌握，面试必考（不一定全考）\
2.梳理知识点，从荣昌的文档中摘出考点和重点\
3.考察形式不限（参考后边的真题）但都在范围内

#### 指令、插值

1.插值、表达式\
2.指令、动态属性\
3.v-html:会有XSS风险，会覆盖子组件

![](http://cdn.processon.com/5e8829b7e4b0a1e6dcb28b5e?e=1585985479\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:5kMNRbrmc0i1YwFOxG51FITHH-U=)

#### computed和watch

1.computed有缓存，data不变不会重新重新计算\
2.watch如何深度监听?\
3.watch监听引用类型，拿不到oldValcomputed缓存可以提性能

**ComputedDemo**

![](http://cdn.processon.com/5e885439e4b03404567d083a?e=1585996361\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:dmM1uABV6qWHPrUO5x-kG9TeYUs=)

watch默认是浅监听的\
name是值类型，可正常拿到 oldVal 和 val\
info是引用类型，拿不到 oldVal 。因为指针相同，此时已经指向了新的 val

#### class和style

1.使用动态属性\
2.使用驼峰式写法

**ClassDemo**

![](http://cdn.processon.com/5e885508e4b064d902cfacf1?e=1585996569\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:\_EHzqahXxP8HrQUEvtKk19LqtLU=)

#### 条件渲染

1.v-if v-else的用法，可使用变量，也可以使用===表达式\
2.v-if和v-show的区别\
3.v-if和v-show的使用场景(dom节点销毁频繁时选择v-show)

### 3 vue基本知识点串讲

#### 循环（列表）渲染

1.如何遍历对象？——也可以用v-for\
2.key的重要性，key不能乱写（如random或者index）\
3.v-for和v-if不能一起使用！

**ListDemo**

![](http://cdn.processon.com/5e8858abe4b0bf3ebcf7caaa?e=1585997499\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:jrs-EQlsRAO\_tpQaHx1MU92k6wQ=)

a b c都是和业务相关的id

#### 事件

1.event参数，自定义参数\
2.事件修饰符，按键修饰符\
3.【观察】事件被绑定到哪里？

**EventDemo**

![](http://cdn.processon.com/5e885ae4e4b0bf3ebcf7ceb5?e=1585998069\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:C5eXZVNfh6M7IzsVKWyP-f-wV54=)

事件中传自定义参数：   @click="increment2(2, $event)"console.log(event.target)\
事件挂在什么地方： console.log('event', event, event.\_\_proto\_\_.constructor)\
event打印出来是MouseEvent，MouseEvent是原生的 event 对象![](http://cdn.processon.com/5e885b64e4b07e41dc2afedb?e=1585998196\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:07as6tCyyDwXVELasb3L\_mucLNA=)

#### 修饰符

![](http://cdn.processon.com/5e885ee9e4b07e41dc2b077a?e=1585999098\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:TikzkgCXRAri\_QuUD161eOaEmiA=)![](http://cdn.processon.com/5e885f10e4b03404567d1ddc?e=1585999136\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:scgfJlNeXZc5PBoF2bDGaA4hWKU=)

#### 表单

1.v-model\
2.常见表单项 textarea checkbox radio select\
3.修饰符 lazy  number trimFormDemo

![](http://cdn.processon.com/5e886200e4b064d902cfc886?e=1585999888\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:RJzhSedb2H0mBAmxobmTgXzqZ6U=)

修饰符

![](http://cdn.processon.com/5e886127e4b03bfcd07ef2ef?e=1585999672\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:l8o3kbGq-x\_\_sgQluhd3E\_TEsPA=)

### 4 vue父子组件如何通讯

#### Vue组件使用

1.props和$emit\
2.组件间通讯-自定义事件\
3.组件生命周期

#### vue父子组件如何通讯

proms 父组件->子组件，传递一个信息\
$emit 子组件->父组件，触发一个事件

**示例**：\
Index是父组件，\
Input和List是其子组件，\
Input和List互为兄弟组件

子组件Input.vue

![](http://cdn.processon.com/5e887f8fe4b09396a49ebc48?e=1586007455\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:gOmIdaVa6kN\_FRcUC5Yexkrpauo=)

// 调用父组件的事件\
this.$emit('add', this.title)父组件Index

![](http://cdn.processon.com/5e887fc9e4b0bf3ebcf80f5e?e=1586007514\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:iGbprxBzeZWHRjG9LRtuMz-IdUk=)

### 5 如何用自定义事件进行vue组件通讯

eventevent是vue的一个示例\
已经具备了$on $emit自定义事件的能力，所以不需要引入eventbus

示例：\
Index是父组件，\
Input和List是其子组件，\
Input和List互为兄弟组件父组件Index\
见3-4中图片

子组件Input\
见3-4中图 // 调用自定义事件\
event.$emit('onAddTitle', this.title)

子组件List

![](http://cdn.processon.com/5e888169e4b03231c715b4b9?e=1586007930\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:\_Nw4q0qCOS6L6Qcw21sSOM82gz8=)&#x20;

// 绑定自定义事件\
event.$on('onAddTitle', this.addTitleHandler)        // 及时销毁，否则可能造成内存泄露\
event.$off('onAddTitle', this.addTitleHandler)beforeDestroy的使用场景：及时解绑自定义事件

### 6 vue父子组件生命周期调用顺序

#### 生命周期图示

![](http://cdn.processon.com/5e888404e4b03231c715b9b3?e=1586008596\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:RoxGi9Z6w5aph3Wurbk5d-3Xlbo=)

#### beforeDestroy中要可能要做什么？

解除绑定，销毁子组件以及事件监听器。\
自定义事件的绑定要解除；比如setTimeout定时任务要销毁；\
自己绑定的window或document的事件要销毁；该销毁的不要遗留在内存中

#### created和mounted有什么区别？

created是把vue的实例初始化，只存在于JS内存的一个变量而已，并没有开始渲染；\
mounted是真正在网页上绘制完成，页面已经渲染完，所以大部分都是要在mounted里进行一些操作；

#### 生命周期（单个组件）

挂载阶段\
更新阶段\
销毁阶段\
创建阶段？

#### 生命周期（父子组件）

父子组件的生命周期调用顺序

创建、渲染顺序

创建初始化实例是从外到内的，但是渲染是从内到外的。\
父 beforeCreate\
父 created\
父 beforeMount\
子 beforeCreate\
子 created\
子 beforeMount\
子 mounted\
父 mounted

更新顺序

父 beforeUpdate\
子 beforeUpdate\
子 updated\
父 updated

销毁顺序

父 beforeDestroy\
子 beforeDestroy\
子 destroyed\
父 destroyed

### 7 面试会考察哪些vue高级特性

#### Vue高级特性：

不是每个都很常用，但用到的时候必须要知道\
考察候选人对Vue的掌握是否全面，且有深度\
考察做过的项目是否有深度和复杂度（至少能用到高级特性）

自定义v-model\
$nextTick\
refs\
slot\
动态、异步组件（很多面试者不知道）\
keep-alive\
mixin

### 8 vue如何自己实现v-model

v-model

链接： [https://cn.vuejs.org/v2/guide/components-custom-events.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E7%9A%84-v-model](https://cn.vuejs.org/v2/guide/components-custom-events.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E7%9A%84-v-model)

一个组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件，但是像单选框、复选框等类型的输入控件可能会将 value attribute 用于不同的目的。model 选项可以用来避免这样的冲突：

示例

父组件Index \
自定义组件&#x20;

子组件CustomVModel

![](http://cdn.processon.com/5e889281e4b03bfcd07f4879?e=1586012306\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:qFWm6ARWE4Di8-q1SUMuE0HdGgY=)

v-model="name"\
Index.vue中name的值将会传入CustomVModel.vue中（model里名为 text1的 prop）。\
同时当CustomVModel.vue触发一个 change 事件并附带一个新的值的时候，这个name的属性将会被更新。注意你仍然需要在组件的 props 选项里声明 text1这个 prop。

### 9 vue组件更新之后如何获取最新DOM

$nextTick:

Vue是异步渲染（原理部分会详细讲解，React也是异步渲染）\
data改变之后，DOM不会立刻渲染\
$nextTick会在DOM渲染之后被触发，以获取最新DOM节点在this.$nextTick(() => {\
&#x20;   //在传入的函数中进行操作\
})\
\
vm.$nextTick( \[callback] )\
将回调延迟到下次 DOM 更新循环之后执行。在修改数据之后立即使用它，然后等待 DOM 更新。\
它跟全局方法 Vue.nextTick 一样，不同的是回调的 this 自动绑定到调用它的实例上。

示例

![](http://cdn.processon.com/5e889811e4b0a1e6dcb35e0f?e=1586013729\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:72rmM4SopbRxc3zgbXbB\_xo5J9Y=)

### 10 slot是什么

#### slot

基本使用\
作用域插槽\
具名插槽

**slot的作用**：让父组件可以往子组件中插入一段内容（不一定是字符串，可以是其它的组件，只要是符合Vue标准的组件或者标签都可以）

示例

插槽内容

![](http://cdn.processon.com/5e88a91be4b03231c715fc48?e=1586018091\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:ZpVRhlAatn-kEDf8TYsxmRjudlM=)

slot标签内用来接收在父组件中插入的\{{website.title\}}，\
当组件渲染的时候，\<slot>\</slot> 将会被替换为'imooc'\
插槽的作用就是在使用组件时，可以把一些子内容插到组件内的slot标签中，代替slot;\
如果不插入内容，就会使用slot中的默认内容。

#### 作用域插槽

![](http://cdn.processon.com/5e88a894e4b07e41dc2b87e2?e=1586017956\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:TAjzz0qpzrZuPBLQE4QoebnUmSM=)

作用域插槽的作用：让父组件可以访问到子组件的数据（不是很常考，但是要知道）\
\
在子组件内部的slot标签上绑定动态数据:slotData="website"\
在父组件中的ScopedSlotDemo组件中插入template，v-slot="slotProps"，通过slotProps.slotData获取到子组件中的website数据

#### 具名插槽

![](http://cdn.processon.com/5e88ab94e4b09396a49f08ef?e=1586018725\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:eeRkn4aMmE7KfT7z3k-iekiT1FQ=)

多个插槽时，给slot加上name，可以通过name和v-slot对应，没有命名的相互对应\
\
v-slot:header可以简写为#header

### 11 vue动态组件是什么

#### 动态组件

1\. :is='component-name'用法\
2\. 需要根据数据，动态渲染的场景。即组件类型不确定。

#### 使用场景

![](http://cdn.processon.com/5e88ac40e4b064d902d047d7?e=1586018896\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:opY4SfpLz7SGfecrGGk551xOmPE=)

比如规范落地页（新闻落地页），图文视频组件的不同排列组合。

#### 示例

![](http://cdn.processon.com/5e88ade6e4b0a1e6dcb37f4e?e=1586019318\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:PB0fEOAd1c2o77uxc6OWTHntriQ=)![](http://cdn.processon.com/5e88ae0fe4b03404567da480?e=1586019359\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:QftztdjwEgvi0kGf21CmFneb0cQ=)

### 12 vue如何异步加载组件

#### 异步组件（很常用）

1.import函数\
2.按需加载，异步加载大组件

#### 示例

![](http://cdn.processon.com/5e88afc9e4b03bfcd07f75bc?e=1586019801\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:vbIvQJX0bYSaoNHuyxeld1ELbYY=)

import CustomVModel from './CustomVModel'\
这种引入方式为同步加载，打包时也是打一个包出来\
\
异步组件引入方式：\
直接在components中注册\
FormDemo: () => import('../BaseUse/FormDemo')\
异步组件只有在用到的时候才会加载\
点击按钮，showFormDemo变为true，FormDemo才会加载

### 13 vue如何缓存组件

#### keep-alive

1.缓存组件\
2.频繁切换，不需要重复渲染\
3.Vue常见性能优化

#### 使用场景

常见的tab切换使用keep-alive

#### 示例

![](http://cdn.processon.com/5e88b301e4b0bf3ebcf86465?e=1586020625\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:Rji9f4zOEcIQsNVDkCML4Y318W0=)

如果去掉\<keep-alive>切换tab时，会先销毁当前的组件，再挂在新的组件![](http://cdn.processon.com/5e88b364e4b0bf3ebcf864a6?e=1586020724\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:yVyI7MFVARflRTJ\_fazv4t2xMs0=)

#### keep-alive和v-show的区别：

v-show是通过css样式display控制隐藏显示DOM\
keep-alive是vue框架层级进行的js对象的渲染（一个组件就是一个js对象）

\--原本组件会有Mounted和beforeDestory去渲染销毁。要是我们只要渲染，而不去销毁，比如带有层级的复杂组件，我们用keep-alive去包裹起来进行缓存，切换组件直接从缓存读取，大大提高了性能。\
\--对于简单的组件，我们就直接使用v-show去操作好了

### 14 vue组件如何抽离公共逻辑

#### mixin

1.多个组件有相同的逻辑，抽离出来\
2.mixin并不是完美的解决方案，会有一些问题\
3.Vue3提出的Component API 旨在解决这些问题

#### 示例

![](http://cdn.processon.com/5e88b5ede4b03404567daaa4?e=1586021374\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:qm379fAAbknSfldIHz5ZfbHygIw=)

在组件中引入mixin的js文件   import myMixin from './mixin'\
mixins:\[myMixin] //可以添加多个，会自动合并起来mixin.js文件中的配置信息会跟引入mixin的组件的配置信息进行混合，混合完之后生成一个整体。

#### mixin问题

1.变量来源不明确，不利于阅读（mixin中的变量或者方法在当前组件是查不到的）\
2.多mixin可能会造成命名冲突（如data变量，方法名称，只要是有名称的都有可能冲突，但是像mounted函数不会冲突，这是vue特有的生命周期，里面的代码会合并）\
3.mixin和组件可能出现多对多的关系，复杂度较高（一个组件引多个mixin，多个组件引用一个mixin）

### 15 vue高级特性知识点小结

#### 相关面试技巧

1.可以不太深入，但必须知道\
2.熟悉基本用法，了解使用场景\
3.最好能和自己的项目经验结合起来

### 16 vuex知识点串讲

#### Vuex使用

1.面试考点并不多（因为熟悉Vue之后，vuex没有难度）\
2.但基本概念、基本使用和API必须要掌握\
3.可能会考察state的数据结构设计

#### Vuex基本概念

state\
getters\
action\
mutation

#### 用于Vue组件

dispatch\
commit\
mapState\
mapGetters\
mapActions\
mapMutations

#### Vuex必会图

![](http://cdn.processon.com/5e88b86ce4b0a1e6dcb3881e?e=1586022013\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:cukEwBTZJOFjXdPNwUYPdRwZqgE=)

Actions里才能做异步操作，常用语ajax请求\
Mutations是同步操作，力求最小化

### 17 vue-router知识点串讲

#### Vue-router使用

1.面试考点并不多（前提熟悉Vue）\
2.路由模式（hash、 H5 history）\
3.路由配置（动态路由、懒加载）

#### Vue-router路由模式

1\. hash模式（默认）,如http://abc.com/#/user/10\
2\. H5 history模式，如http://abc.com/user/20\
3\. 后者需要server支持，因此无特殊需求可选择前者

#### Vue-router路由模式配置

![](http://cdn.processon.com/5e88ba4de4b0a1e6dcb38983?e=1586022493\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:Gt0H9YO1NRJYOllc-WXpusJOQ5E=)

#### Vue-router路由配置

动态路由

![](http://cdn.processon.com/5e88bc84e4b03bfcd07f7f18?e=1586023062\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:kDIq8XiQHR-MUT9sIk-XuIeeYO4=)

懒加载

![](http://cdn.processon.com/5e88bcade4b064d902d055d3?e=1586023102\&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:gSW\_8OY6Q50eo0K1tYQJ21qWleE=)

#### 总结

1.面试考点并不多（前提是熟悉vue）\
2.掌握基本概念，基本使用\
3.面试官时间有限，需考察最核心、最常用的问题，而非边角问题

### 18 vue使用-考点总结和复习

#### v-show和v-if的区别

v-show：节点一直存在，通过css的display控制展示状态，\
v-if：节点会根据v-if的值来动态的创建和销毁\
组件频繁切换显示状态时，使用v-show，可以降低渲染消耗\
组件创建以后，不再频繁切换显示状态时使用v-if

#### vue组件如何通讯

1.父子组件，使用属性和触发事件\
2.组件之间无关或者层级较深时，使用自定义事件\
3.Vuex通讯\

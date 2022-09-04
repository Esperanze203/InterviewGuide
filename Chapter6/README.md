# JavaScript/ES6

### **一、JS数组常用方法**

|             方法            |                     说明                     |
| :-----------------------: | :----------------------------------------: |
|           push()          |                  添加元素到数组末尾                 |
|           pop()           |                  删除数组末尾元素                  |
|         unshift()         |                 添加元素到数组的头部                 |
|          shift()          |                  删除数组最前面元素                 |
|         indexOf()         |                查看某个元素在数组中的位置               |
| splice(start, num, value) | 实现增删改操作（start开始下标，num删除元素个数，value插入或替换的元素） |
|     slice(begin, end)     |               浅拷贝数组并返回拷贝后的新数组              |
|        Array.from()       |          从一个类似数组或可迭代对象中创建一个新的数组实例          |
|  fill(value, start, end)  |        用一个固定值填充数组中\[start,end)的全部元素        |

### **二、mouseover和mouseenter的区别**

mouseover/mouseout：当鼠标移入元素或其子元素都会触发事件，有一个重复触发的冒泡过程

mouseenter/mouseleave：当鼠标移入元素本身（不包含元素的子元素）会触发事件，即不会冒泡

### **三、clientHeight, scrollHeight, offsetHeight ,以及scrollTop, offsetTop, clientTop的区别？**

clientHeight：可视区域高度，不包含border和滚动条\
offsetHeight： 可视区域高度，包含border和滚动条\
scrollHeight：所有区域高度，包含因滚动被隐藏的部分\
clientTop：边框border的厚度\
scrollTop：滚动后被隐藏的高度，获取对象最顶端与窗口中可见内容最顶端之间的距离\
offsetTop：获取指定对象相对于版面或布局中设置position属性的父容器顶端位置的距离

![](../.gitbook/assets/浏览器宽高.jpg)

### ****

### **八、ES6有哪些新特性？**

* 新增let、const声明变量，实现了块级作用域
* 新增箭头函数
* 引入promise、await/async解决异步回调问题
* 引入Class作为对象的模板，实现更好的面向对象编程
* 引入模块方便模块化编程
* 引入新的数据类型symbol，新的数据结构set和map

### ****

### **十一、setTimeout、setInterval和requestAnimationFrame**

|             名称            |                                                                                         说明                                                                                        |
| :-----------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|  setTimeout/clearTimeout  |                                                                                     延时执行参数指定代码                                                                                    |
| setInterval/clearInterval |                                                                                    每隔一段时间执行指定代码                                                                                   |
|   requestAnimationFrame   | 在浏览器每次刷新页面之前执行：1. 会把每一帧中所有的DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率；2. 对于隐藏元素不会进行重绘或回流，减少了CPU、GPU和内存使用量；3. 由浏览器专门为动画提供的API，在运行时浏览器会自动优化方法的调用；页面如果不是激活状态，动画会暂停播放，有效节省了CPU开销 |

### **十二、高频度触发事件的优化方案**

| 方案         | 说明                    | 应用场景          |
| ---------- | --------------------- | ------------- |
| 防抖debounce | 抖动结束的时间超过指定时间间隔时才执行任务 | 搜索联想、窗口resize |
| 节流throttle | 指定时间间隔内只执行一次任务        | 滚动事件、鼠标不断点击触发 |

### ****

### ****

### **十九、如何理解前端模块化**&#x20;

模块化思想：隔离不同的js文件，仅暴露当前模块所需要的其他模块

将复杂的文件编成一个个独立的模块，有利于复用和维护。但会产生模块之间相互依赖的问题，可通过js打包工具webpack解决

### **二十、ES6模块化**

1. ES6模块中自动采用严格模式，规定：
   * 变量必须先声明
   * 函数参数不能有同名属性
   * 禁止this指向全局
   * 对只读属性赋值、删除不可删除属性直接报错
   * arguments不可重新赋值，不会自动反应函数参数变化
   * 增加保留字static、interface、product
2. export export语句输出的接口是对应值的引用，也就是一种动态绑定关系，通过该接口可以获取模块内部实时的值；export命令要处于模块顶层
   * 把export直接加到声明前面
   * export {a, b, c}
   * export default默认导出（一个js文件中只能有一个默认导出，但可以导出多个方法）
3. import import是静态执行，Singleton模式；import命令要处于模块顶层
   * import {XX} from ‘./test.js’
   * import {XX as YY} from ‘./test.js’
   * import \* as YY from ‘./test.js’

### **二十一、webpack用来干什么的**

js应用程序的静态模块打包器。当用webpack处理应用程序时，它会递归地构建一个依赖关系图，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个bundle

### ****

### **二十七、**<mark style="color:red;">**跨域**</mark>**原理？js实现跨域？**

**跨域**：浏览器不能执行其他网站的脚本，是由浏览器的同源策略造成的，是浏览器对JS实施的安全限制\
（只要协议、域名、端口有任何一个不同，都被当作是不同的域）

**跨域原理**：通过各种方式避开浏览器的安全限制

**实现方法**：CORS；代理服务器；JSONP；document.domain+iframe；location.hash+iframe；window.name+iframe；postMessage

### ****

### ****

### ****

### **三十四、什么是事件委托/事件代理？典型例子？**&#x20;

**定义**：不在事件发生的直接DOM上设置监听函数，而在其父元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过判断事件发生元素DOM的类型（使用target属性），来做出不同的响应。

**好处**：新增子对象时无需再次对其绑定事件，适合动态添加元素；减少事件注册，减少内存消耗。

**举例**：ul和li标签的事件监听（不在li标签上直接添加事件监听而是在ul标签上添加）

### **三十五、什么是事件监听**&#x20;

<mark style="color:orange;">**element.addEventListener**</mark><mark style="color:orange;">(event, function, useCapture)</mark> 用于向指定元素添加事件&#x20;

* event：事件类型，如click、scroll、mousedown、resize等&#x20;
* function：事件触发后调用的函数&#x20;
* useCapture：描述事件传递方式，可选。默认为false即冒泡传递；true时为捕获传递

### ****

### **三十八、说一下JS的事件模型**

1.  事件模型

    *   DOM0事件模型/原始事件模型：事件不会传播，仅作为元素的一个属性

        直接在HTML中绑定：

        ```
        ```

    &#x20;\`\`\`

    通过js代码指定属性值：

    ```
    var btn = document.getElementById('.btn'); btn.onclick = fun;
    ```

    移除监听函数：

    ```
    btn.onclick=null;
    ```

    * IE事件模型：事件处理阶段→事件冒泡阶段（目标元素→document） 绑定：attachEvent(eventType, handler) 移除：detachEvent(eventType, handler)
    * DOM2事件模型：事件捕获阶段→事件处理阶段→事件冒泡阶段（document→目标元素→document） 绑定：addEventListener(eventType, handler, useCapture) 移除：removeEventListener(eventType, handler, useCapture)
2. 事件对象
   * DOM事件模型中的事件对象常用属性 type获取事件类型 target获取事件的目标节点 stopPropagation()阻止捕获和冒泡阶段中当前事件的进一步传播 preventDefault()阻止事件默认行为而不停止事件的进一步传播
   * IE事件模型中的事件对象常用属性 type获取事件类型 srcElement获取事件目标 cancelBubble阻止事件冒泡 returnValue阻止事件默认行为
3.  执行顺序

    如果一个DOM节点同时绑定了多个事件监听函数，且有的用于捕获，有的用于冒泡，则绑定在被点击元素上的事件是按照代码添加顺序执行的，其他先捕获再冒泡。

### ****

### **四十二、说说C++，Java，JavaScript这三种语言的区别**

*   静态类型/动态类型

    C++、Java属于静态类型语言，编译的时候就能够知道每个变量的类型，编程时需给定类型；js属于动态类型语言，运行的时候才知道每个变量的类型，编程的时候无需显示指定的类型
*   编译型/解释型

    C++是编译型语言，需要编译器编译成本地可执行程序后才能运行，用户只使用编译好的本地代码；js是解释型语言，用户直接使用脚本解释器将脚本文件解释执行；Java分为两个阶段，首先像C++一样经过编译器编译，但生成字节码（与平台无关），然后由Java虚拟机运行字节码，使用解释器执行这些代码
*   js和Java的区别：

    Java编译字节码阶段和执行阶段是分开的，即编译阶段时间长短无所谓；对于js这些都是在网页和js文件下载后同执行阶段一起在网页的加载和渲染过程中实施的，所以对处理时间有严格要求

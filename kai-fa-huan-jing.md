# 开发环境

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

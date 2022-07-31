# JavaScript基础

### 一、JS数据类型

**值类型(基本类型)**：字符串（String）、数字(Number)、布尔(Boolean)、空（Null）、未定义（Undefined）、Symbol。

**引用数据类型（对象类型）**：对象(Object)、数组(Array)、函数(Function)，还有两个特殊的对象：正则（RegExp）和日期（Date）。

**注：**<mark style="color:red;">Symbol</mark> 是 ES6 引入了一种新的原始数据类型，表示独一无二的值。

![](../.gitbook/assets/Javascript-DataType.png)

#### JavaScript 拥有动态类型

JavaScript 拥有动态类型。这意味着相同的变量可用作不同的类型。

#### Undefined 和 Null

Undefined 这个值表示变量不含有值。

可以通过将变量的值设置为 null 来清空变量。

### 二、创建 Boolean 对象

Boolean 对象代表两个值:"true" 或者 "false"

下面的代码定义了一个名为 myBoolean 的布尔对象：

```javascript
var myBoolean = new Boolean();
```

如果布尔对象**无初始值**或者其值为:

* **0**
* **-0**
* **null**
* **""**
* **false**
* **undefined**
* **NaN**

那么对象的值为 **false**。否则，其值为 **true**（即使当变量值为字符串 "false" 时）！

### 三、[数组的常见方法](https://web.qianguyihao.com/04-JavaScript%E5%9F%BA%E7%A1%80/19-%E6%95%B0%E7%BB%84%E7%9A%84%E5%B8%B8%E8%A7%81%E6%96%B9%E6%B3%95.html#%E6%95%B0%E7%BB%84%E7%9A%84%E6%96%B9%E6%B3%95%E6%B8%85%E5%8D%95)

#### 数组的类型相关 <a href="#shu-zu-de-lei-xing-xiang-guan" id="shu-zu-de-lei-xing-xiang-guan"></a>

| 方法                               | 描述                  |
| -------------------------------- | ------------------- |
| Array.isArray()                  | 判断是否为数组             |
| toString()                       | 将数组转换为字符串           |
| Array.from(arrayLike)            | 将**伪数组**转化为**真数组**  |
| Array.of(value1, value2, value3) | 创建数组：将**一系列值**转换成数组 |

注意，获取数组的长度是用`length`属性，不是方法。关于 `length`属性，详见上一篇文章。

#### [#](https://web.qianguyihao.com/04-JavaScript%E5%9F%BA%E7%A1%80/19-%E6%95%B0%E7%BB%84%E7%9A%84%E5%B8%B8%E8%A7%81%E6%96%B9%E6%B3%95.html#%E6%95%B0%E7%BB%84%E5%85%83%E7%B4%A0%E7%9A%84%E6%B7%BB%E5%8A%A0%E5%92%8C%E5%88%A0%E9%99%A4) 数组元素的添加和删除 <a href="#shu-zu-yuan-su-de-tian-jia-he-shan-chu" id="shu-zu-yuan-su-de-tian-jia-he-shan-chu"></a>

| 方法        | 描述                                        | 备注      |
| --------- | ----------------------------------------- | ------- |
| push()    | 向数组的**最后面**插入一个或多个元素，返回结果为新数组的**长度**      | 会改变原数组  |
| pop()     | 删除数组中的**最后一个**元素，返回结果为**被删除的元素**          | 会改变原数组  |
| unshift() | 在数组**最前面**插入一个或多个元素，返回结果为新数组的**长度**       | 会改变原数组  |
| shift()   | 删除数组中的**第一个**元素，返回结果为**被删除的元素**           | 会改变原数组  |
| slice()   | 从数组中**提取**指定的一个或多个元素，返回结果为**新的数组**        | 不会改变原数组 |
| splice()  | 从数组中**删除**指定的一个或多个元素，返回结果为**被删除元素组成的新数组** | 会改变原数组  |
| fill()    | 填充数组：用固定的值填充数组，返回结果为**新的数组**              | 会改变原数组  |

#### [#](https://web.qianguyihao.com/04-JavaScript%E5%9F%BA%E7%A1%80/19-%E6%95%B0%E7%BB%84%E7%9A%84%E5%B8%B8%E8%A7%81%E6%96%B9%E6%B3%95.html#%E6%95%B0%E7%BB%84%E7%9A%84%E5%90%88%E5%B9%B6%E5%92%8C%E6%8B%86%E5%88%86) 数组的合并和拆分 <a href="#shu-zu-de-he-bing-he-chai-fen" id="shu-zu-de-he-bing-he-chai-fen"></a>

| 方法       | 描述                           | 备注       |
| -------- | ---------------------------- | -------- |
| concat() | 合并数组：连接两个或多个数组，返回结果为**新的数组** | 不会改变原数组  |
| join()   | 将数组转换为字符串，返回结果为**转换后的字符串**   | 不会改变原数组  |
| split()  | 将字符串按照指定的分隔符，组装为数组           | 不会改变原字符串 |

注意，`split()`是字符串的方法，不是数组的方法。

#### [#](https://web.qianguyihao.com/04-JavaScript%E5%9F%BA%E7%A1%80/19-%E6%95%B0%E7%BB%84%E7%9A%84%E5%B8%B8%E8%A7%81%E6%96%B9%E6%B3%95.html#%E6%95%B0%E7%BB%84%E6%8E%92%E5%BA%8F) 数组排序 <a href="#shu-zu-pai-xu" id="shu-zu-pai-xu"></a>

| 方法        | 描述                                 | 备注     |
| --------- | ---------------------------------- | ------ |
| reverse() | 反转数组，返回结果为**反转后的数组**               | 会改变原数组 |
| sort()    | 对数组的元素,默认按照**Unicode 编码**，从小到大进行排序 | 会改变原数组 |

#### [#](https://web.qianguyihao.com/04-JavaScript%E5%9F%BA%E7%A1%80/19-%E6%95%B0%E7%BB%84%E7%9A%84%E5%B8%B8%E8%A7%81%E6%96%B9%E6%B3%95.html#%E6%9F%A5%E6%89%BE%E6%95%B0%E7%BB%84%E7%9A%84%E5%85%83%E7%B4%A0) 查找数组的元素 <a href="#cha-zhao-shu-zu-de-yuan-su" id="cha-zhao-shu-zu-de-yuan-su"></a>

| 方法                    | 描述                                           | 备注                                |
| --------------------- | -------------------------------------------- | --------------------------------- |
| indexOf(value)        | 从前往后索引，检索一个数组中是否含有指定的元素                      |                                   |
| lastIndexOf(value)    | 从后往前索引，检索一个数组中是否含有指定的元素                      |                                   |
| includes(item)        | 数组中是否包含指定的内容                                 |                                   |
| find(function())      | 找出**第一个**满足「指定条件返回 true」的元素                  |                                   |
| findIndex(function()) | 找出**第一个**满足「指定条件返回 true」的元素的 index           |                                   |
| every()               | 确保数组中的每个元素都满足「指定条件返回 true」，则停止遍历，此方法才返回 true | 全真才为真。要求每一项都返回 true，最终的结果才返回 true |
| some()                | 数组中只要有一个元素满足「指定条件返回 true」，则停止遍历，此方法就返回 true  | 一真即真。只要有一项返回 true，最终的结果就返回 true   |

#### [#](https://web.qianguyihao.com/04-JavaScript%E5%9F%BA%E7%A1%80/19-%E6%95%B0%E7%BB%84%E7%9A%84%E5%B8%B8%E8%A7%81%E6%96%B9%E6%B3%95.html#%E9%81%8D%E5%8E%86%E6%95%B0%E7%BB%84) 遍历数组 <a href="#bian-li-shu-zu" id="bian-li-shu-zu"></a>

| 方法        | 描述                                       | 备注                                                              |
| --------- | ---------------------------------------- | --------------------------------------------------------------- |
| for 循环    | 这个大家都懂                                   |                                                                 |
| forEach() | 和 for 循环类似，但需要兼容 IE8 以上                  | forEach() 没有返回值。也就是说，它的返回值是 undefined                           |
| map()     | 对原数组中的每一项进行加工，将组成新的数组                    | 不会改变原数组                                                         |
| filter()  | 过滤数组：返回结果是 true 的项，将组成新的数组，返回结果为**新的数组** | 不会改变原数组                                                         |
| reduce    | 接收一个函数作为累加器，返回值是回调函数累计处理的结果              | [JS reduce 函数](https://juejin.im/post/5d78aa3451882521397645ae) |

### 四、JS精度丢失

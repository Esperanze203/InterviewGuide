# 0-1背包



### 01 背包 <a href="#01-bei-bao" id="01-bei-bao"></a>

有n件物品和一个最多能背重量为w 的背包。第i件物品的重量是weight\[i]，得到的价值是value\[i] 。**每件物品只能用一次**，求解将哪些物品装入背包里物品价值总和最大。

![动态规划-背包问题](https://img-blog.csdnimg.cn/20210117175428387.jpg)

举一个例子：

背包最大重量为4。物品为：

|     | 重量 | 价值 |
| --- | -- | -- |
| 物品0 | 1  | 15 |
| 物品1 | 3  | 20 |
| 物品2 | 4  | 30 |

问背包能背的物品最大价值是多少？

以下讲解和图示中出现的数字都是以这个例子为例。

### 二维dp数组 <a href="#er-wei-dp-shu-zu-01-bei-bao" id="er-wei-dp-shu-zu-01-bei-bao"></a>

[思路解析](https://programmercarl.com/%E8%83%8C%E5%8C%85%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%8001%E8%83%8C%E5%8C%85-1.html#%E4%BA%8C%E7%BB%B4dp%E6%95%B0%E7%BB%8401%E8%83%8C%E5%8C%85)

dp数组以及下标的含义: 使用二维数组，即**dp\[i]\[j] 表示从下标为\[0-i]的物品里任意取，放进容量为j的背包，价值总和最大是多少**。

![](<../../.gitbook/assets/image (1).png>)

js代码：

```javascript
z// Some code
function testWeightBagProblem (weight, value, size) {
    // 定义 dp 数组
    const len = weight.length,
    dp = Array(len).fill().map(() => Array(size + 1).fill(0));
    // 初始化
    // for(let i=0;i<len;i++){ dp[i][0]=0; }
    for(let j=1;j<=size;j++){ dp[0][j]=j>=weight[0]?value[0]:0; }
    // 动规循环
    for(let i=1;i<len;i++){
        for(let j=1;j<=size;j++){
            if(weight[i]<=j){ //重量i<当前容量j：max(放入i发情况，不放i的情况)
                dp[i][j]=Math.max(value[i]+dp[i-1][j-weight[i]],dp[i-1][j]);
            }else{ //重量i<当前容量j：直接等于不放入物品i的情况
                dp[i][j]=dp[i-1][j];
            }
        }
    }
    // console.table(dp);
    return dp[len-1][size]
```

### 一维dp数组（<mark style="color:red;">滚动数组</mark>） <a href="#yi-wei-dp-shu-zu-gun-dong-shu-zu" id="yi-wei-dp-shu-zu-gun-dong-shu-zu"></a>

对于背包问题其实状态都是可以压缩的。

在使用二维数组的时候，递推公式：dp\[i]\[j] = max(dp\[i - 1]\[j], dp\[i - 1]\[j - weight\[i]] + value\[i]);

**其实可以发现如果把dp\[i - 1]那一层拷贝到dp\[i]上，表达式完全可以是：dp\[i]\[j] = max(dp\[i]\[j], dp\[i]\[j - weight\[i]] + value\[i]);**

**与其把dp\[i - 1]这一层拷贝到dp\[i]上，不如只用一个一维数组了**，只用dp\[j]（一维数组，也可以理解是一个<mark style="color:red;">滚动数组</mark>）。

这就是滚动数组的由来，需要满足的条件是上一层可以重复利用，直接拷贝到当前层。

[思路](https://programmercarl.com/%E8%83%8C%E5%8C%85%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%8001%E8%83%8C%E5%8C%85-2.html#%E4%B8%80%E7%BB%B4dp%E6%95%B0%E7%BB%84-%E6%BB%9A%E5%8A%A8%E6%95%B0%E7%BB%84)

代码：

```javascript
// Some code
function testWeightBagProblem (weight, value, size) {
    // 定义 dp 数组
    const len = weight.length,
    // dp = Array(len).fill().map(() => Array(size + 1).fill(0));
    dp=new Array(size+1).fill(0);
    // 初始化
    // for(let i=0;i<len;i++){ dp[i][0]=0; }
    // for(let j=1;j<=size;j++){ dp[0][j]=j>=weight[0]?value[0]:0; }
    for(let j=1;j<=size;j++){ dp[j]=j>=weight[0]?value[0]:0; }
    // 动规循环
    for(let i=1;i<len;i++){
        for(let j=size;j>=1;j--){//倒序遍历，则每次访问的dp[j-w[i]],dp[j]为上一轮(i-1)的结果
            if(weight[i]<=j){
                // dp[i][j]=Math.max(value[i]+dp[i-1][j-weight[i]],dp[i-1][j]);
                dp[j]=Math.max(value[i]+dp[j-weight[i]],dp[j]);
                // console.log("i:"+i+",j:"+j+"dp[j]:"+dp[j])
            }
        }
    }
    // console.table(dp);
    return dp[size];
}
```

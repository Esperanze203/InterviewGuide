# 有序数组的平方

[力扣题目链接](https://leetcode.cn/problems/squares-of-a-sorted-array/)

给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

示例 1： 输入：nums = \[-4,-1,0,3,10] 输出：\[0,1,9,16,100] 解释：平方后，数组变为 \[16,1,0,9,100]，排序后，数组变为 \[0,1,9,16,100]

示例 2： 输入：nums = \[-7,-3,2,3,11] 输出：\[4,9,9,49,121]

## 思路：

### 双指针（左右）

数组其实是有序的， 只不过负数平方之后可能成为最大数了。

那么数组平方的最大值就在数组的两端，不是最左边就是最右边，不可能是中间。

此时可以考虑双指针法了，i指向起始位置，j指向终止位置。

定义一个新数组res，和A数组一样的大小，让idx指向result数组终止位置。

![](../../.gitbook/assets/977.有序数组的平方.gif)

```javascript
// Some code
var sortedSquares = function(nums) {
    let res = new Array(nums.length);
    let left=0,right=nums.length-1,idx=nums.length-1;
    while (left<=right) {
        if(Math.abs(nums[left])>=Math.abs(nums[right])){
            res[idx--] = Math.pow(nums[left++],2) 
        }else{
            res[idx--] = Math.pow(nums[right--],2) 
        }
    }
    return res
}
```


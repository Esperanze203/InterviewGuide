# 二分查找

[力扣题目链接](https://leetcode.cn/problems/binary-search/)

[代码随想录链接](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html#\_704-%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE)

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:

```javascript
输入: nums = [-1,0,3,5,9,12], target = 9     
输出: 4       
解释: 9 出现在 nums 中并且下标为 4     
```

示例 2:

```javascript
输入: nums = [-1,0,3,5,9,12], target = 2     
输出: -1        
解释: 2 不存在 nums 中因此返回 -1        
```

提示：

* 你可以假设 nums 中的所有元素是不重复的。
* n 将在 \[1, 10000]之间。
* nums 的每个元素都将在 \[-9999, 9999]之间。

## 思路 <a href="#si-lu" id="si-lu"></a>

**这道题目的前提是数组为有序数组**，同时题目还强调**数组中无重复元素**，因为一旦有重复元素，使用二分查找法返回的元素下标可能不是唯一的。

二分查找涉及的很多的边界条件，逻辑比较简单。大家写二分法经常写乱，主要是因为**对区间的定义没有想清楚，区间的定义就是不变量**。要在二分查找的过程中，保持不变量，就是在while寻找中每一次边界的处理都要坚持根据区间的定义来操作，这就是**循环不变量**规则。

写二分法，区间的定义一般为两种，<mark style="color:red;">左闭右闭</mark>即**\[left, right]**，或者<mark style="color:red;">左闭右开</mark>即**\[left, right)**。

### 二分法第一种写法（我的写法） <a href="#er-fen-fa-di-yi-zhong-xie-fa" id="er-fen-fa-di-yi-zhong-xie-fa"></a>

第一种写法，我们定义 target 是在一个在左闭右闭的区间里，**也就是**<mark style="color:red;">**\[left, right]**</mark>** （这个很重要非常重要）**。区间的定义这就决定了二分法的代码应该如何写，**因为定义target在\[left, right]区间，所以有如下两点：**

* while (left <= right) 要使用 <= ，因为left == right是有意义的，所以使用 <=
* if (nums\[middle] > target) right 要赋值为 middle - 1，因为当前这个nums\[middle]一定不是target，那么接下来要查找的左区间结束下标位置就是 middle - 1

```javascript
// js写法
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    // right是数组最后一个数的下标，num[right]在查找范围内，是左闭右闭区间
    let left = 0, right = nums.length - 1;
    // 当left=right时，由于nums[right]在查找范围内，所以要包括此情况
    while (left <= right) {
        let mid = left + Math.floor((right - left)/2);
        // 如果中间数大于目标值，要把中间数排除查找范围，所以右边界更新为mid-1；如果右边界更新为mid，那中间数还在下次查找范围内
        if (nums[mid] > target) {
            right = mid - 1;  // 去左面闭区间寻找
        } else if (nums[mid] < target) {
            left = mid + 1;   // 去右面闭区间寻找
        } else {
            return mid;
        }
    }
    return -1;
};
```

```python
# python写法
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        l,r = 0,len(nums)-1  # 定义target在左闭右闭的区间里，[left, right]
        while l<=r:  # 当left==right，区间[left, right]依然有效，所以用 <=
            mid = (l+r) // 2
            if target == nums[mid]:
                return mid
            if target > nums[mid]:
                l = mid+1  # target 在右区间，所以[middle + 1, right]
            else: 
                r = mid-1  # target 在左区间，所以[left, middle - 1]
        # 如果遍历结束还没有找到target，则返回-1
        return -1
```

### 二分法第二种写法 <a href="#er-fen-fa-di-er-zhong-xie-fa" id="er-fen-fa-di-er-zhong-xie-fa"></a>

如果说定义 target 是在一个在左闭右开的区间里，也就是\[left, right) ，那么二分法的边界处理方式则截然不同。有如下两点：

* while (left < right)，这里使用 < ,因为left == right在区间\[left, right)是没有意义的
* if (nums\[middle] > target) right 更新为 middle，因为当前nums\[middle]不等于target，去左区间继续寻找，而寻找区间是左闭右开区间，所以right更新为middle，即：下一个查询区间不会去比较nums\[middle]

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    // right是数组最后一个数的下标+1，nums[right]不在查找范围内，是左闭右开区间
    let left = 0, right = nums.length;    
    // 当left=right时，由于nums[right]不在查找范围，所以不必包括此情况
    while (left < right) {
        let mid = left + Math.floor((right - left)/2);
        // 如果中间值大于目标值，中间值不应在下次查找的范围内，但中间值的前一个值应在；
        // 由于right本来就不在查找范围内，所以将右边界更新为中间值，如果更新右边界为mid-1则将中间值的前一个值也踢出了下次寻找范围
        if (nums[mid] > target) {
            right = mid;  // 去左区间寻找
        } else if (nums[mid] < target) {
            left = mid + 1;   // 去右区间寻找
        } else {
            return mid;
        }
    }
    return -1;
};
```

### 相关题目

[35.搜索插入位置](https://programmercarl.com/0035.%E6%90%9C%E7%B4%A2%E6%8F%92%E5%85%A5%E4%BD%8D%E7%BD%AE.html)

[34.在排序数组中查找元素的第一个和最后一个位置](https://programmercarl.com/0034.%E5%9C%A8%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E6%9F%A5%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%92%8C%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E4%BD%8D%E7%BD%AE.html)

[33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array)




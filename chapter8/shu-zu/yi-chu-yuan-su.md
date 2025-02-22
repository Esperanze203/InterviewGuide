# 移除元素

[力扣题目链接](https://leetcode.cn/problems/remove-element/)

给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并**原地**修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

示例 1: 给定 nums = \[3,2,2,3], val = 3, 函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。 你不需要考虑数组中超出新长度后面的元素。

示例 2: 给定 nums = \[0,1,2,2,3,0,4,2], val = 2, 函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

**你不需要考虑数组中超出新长度后面的元素。**

## **解法**

### 双指针法（快慢指针） <a href="#shuang-zhi-zhen-fa" id="shuang-zhi-zhen-fa"></a>

**快慢指针**： 通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。

**注意：**此方法<mark style="color:red;">**不改变元素的相对位置**</mark>。

定义快慢指针

* 快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组
* 慢指针：指向更新 新数组下标的位置

删除过程如下：

![](../../.gitbook/assets/快慢指针.gif)

```javascript
//时间复杂度：O(n)
//空间复杂度：O(1)
var removeElement = (nums, val) => {
    let k = 0;
    for(let i = 0;i < nums.length;i++){
        if(nums[i] != val){
            nums[k++] = nums[i]
        }
    }
    return k;
};
```

ja删除过程ja如下：j'a​

### 双指针法（左右指针） <a href="#shuang-zhi-zhen-fa" id="shuang-zhi-zhen-fa"></a>

**相向双指针**方法，基于元素顺序可以改变的题目描述<mark style="color:red;">**改变了元素相对位置**</mark>，确保了<mark style="color:orange;">移动最少元素</mark>。

```javascript
/**
* js
* 相向双指针方法，基于元素顺序可以改变的题目描述改变了元素相对位置，确保了移动最少元素
* 时间复杂度：O(n)
* 空间复杂度：O(1)
*/
var removeElement = function(nums, val) {
    let left=0,right=nums.length-1;
    // 借助了一个count来计数，不用count的方法看下面c++版本
    let count=nums.length;
    while(left<=right) {
        // 找右边不等于val的元素
        while(nums[right]==val){
            right--;
            count--;
        }
        // 找左边等于val的元素，并将右边不等于val的元素覆盖左边等于val的元素
        if(left<=right && nums[left] == val){
            nums[left] = nums[right];
            right--;
            count--;
        }
        left++;
    }
    return count
};
```

```cpp
/**
* c++
* 相向双指针方法，基于元素顺序可以改变的题目描述改变了元素相对位置，确保了移动最少元素
* 时间复杂度：O(n)
* 空间复杂度：O(1)
*/
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int leftIndex = 0;
        int rightIndex = nums.size() - 1;
        while (leftIndex <= rightIndex) {
            // 找左边等于val的元素
            while (leftIndex <= rightIndex && nums[leftIndex] != val){
                ++leftIndex;
            }
            // 找右边不等于val的元素
            while (leftIndex <= rightIndex && nums[rightIndex] == val) {
                -- rightIndex;
            }
            // 将右边不等于val的元素覆盖左边等于val的元素
            if (leftIndex < rightIndex) {
                nums[leftIndex++] = nums[rightIndex--];
            }
        }
        return leftIndex;   // leftIndex一定指向了最终数组末尾的下一个元素
    }
};
```

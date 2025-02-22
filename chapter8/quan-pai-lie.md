# 全排列

常见的全排列有两种：1. 输入的是一个字符串；2. 输入的是一个数组。

1. 输入：s = "abc" 输出：\["abc","acb","bac","bca","cab","cba"]
2. 输入: \[1,2,3] 输出: \[\[1,2,3], \[1,3,2], \[2,1,3], \[2,3,1], \[3,1,2], \[3,2,1]]

总体思路都是采用_**回溯算法(BackTracking)**_

> Backtracking is an algorithm for finding all solutions by exploring all potential candidates. If the solution candidate turns to be not a solution (or at least not the last one), backtracking algorithm discards it by making some changes on the previous step.

上面一段话是LeetCode上关于回溯算法的总结，感觉说到了精髓。翻译一下就是：

> 回溯是一种通过探索所有潜在的候选方案来寻找所有解决方案的算法。如果候选的解决方案变成不是解决方案（或者至少不是最后一个），回溯算法通过对上一步进行一些改变，将其舍弃。

该算法在回溯的时候有两种不同的处理方式，下面分别以两种不同的输入参数类型做示范。

```java
/*输入的是一个字符串*/
class Solution {
    private List<String> list = new ArrayList<>();
    public String[] permutation(String s) {
        boolean[] visited = new boolean[s.length()];
        DFS(s, visited, "");
        return list.toArray(new String[list.size()]);
    }
    private void DFS(String s, boolean[] visited, String out) {
        if(out.length() == s.length()) list.add(out);
        else {
            for(int i = 0; i < s.length(); i++) {
                if(visited[i]) continue;
                visited[i] = true;
                DFS(s, visited, out + s.charAt(i));
                visited[i] = false;
            }
        }
    }
}
```

```java
/*输入的是一个数组*/
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> permute(int[] nums) {
        List<Integer> out = new ArrayList<>();
        boolean[] visited = new boolean[nums.length];
        DFS(nums, visited, out);
        return res;
    }
    private void DFS(int[] nums, boolean[] visited, List<Integer> out) {
        if(out.size() == nums.length) res.add(new ArrayList<>(out));
        else {
            for(int i = 0; i < nums.length; i++) {
                if(visited[i]) continue;
                visited[i] = true;
                out.add(nums[i]);
                DFS(nums, visited, out);
                out.remove(out.size() - 1);
                visited[i] = false;
            }
        }
    }
}
```

LeetCode链接：\
https://leetcode-cn.com/problems/permutations/\
https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/

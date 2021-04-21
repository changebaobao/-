---
title: 基础dp
date: 2021-04-15 20:31:55
tags:
 -leetcode刷题记录
categories: 算法
---
### 基础dp，比硬币问题还简单
<!--more-->

## 引言
本来对动态规划的认知约等于0，今天还正好碰到了，什么子问题，最优解，状态转移方程等等等等，反正就是很烦，不过今天碰到的题似乎算是基础中的基础，正文开始
## 基础版<https://leetcode-cn.com/problems/house-robber/>
* 每次选择一个房屋后后，它之前的那个就选不了了，但是之前的前面那个还可以选，类推开始：只有一个时，解唯一，两个时，选择较大的那个，三个是，对于其只有两种情况，选或不选，若选了，则还能选第一个，若不选，则为它前一个的解。。。。。状态转移方程得出
```c++
states[i] = max(states[i - 1], states[i - 2] + nums[i]);
```
* 总的代码
```c++
class Solution {
public:
    int rob(vector<int>& nums)
    {
        int n = nums.size();
        if (n == 0)
            return 0;
        if (n == 1)
            return nums[0];
        vector<int> states = vector<int>(n, 0);
        states[0] = nums[0];
        states[1] = max(nums[0], nums[1]);
        for (int i = 2; i < n; i++) {
            states[i] = max(states[i - 1], states[i - 2] + nums[i]);
        }
        return states[n - 1];
    }
};
```
* 代码进阶，上面那一种感觉已经很简单了，但是之后又看到题解中还有滚顶数组啥的，咱也不太会，复制粘贴纪念一下（以后一定学会）

```c++
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int length = nums.length;
        if (length == 1) {
            return nums[0];
        }
        int first = nums[0], second = Math.max(nums[0], nums[1]);
        for (int i = 2; i < length; i++) {
            int temp = second;
            second = Math.max(first + nums[i], second);
            first = temp;
        }
        return second;
    }
}
```
## 进阶版<https://leetcode-cn.com/problems/house-robber-ii/submissions/
* 进阶版，只不过是需要想的条件多一点而已，第一个选了，最后一个就选不了了，反之。不如直接分为两大组，分别考虑。。。。。。第一次做是直接开了两个状态数组，些许麻烦，直接看官方题解吧(也是用到了滚动数组，嘤嘤嘤)
```c++
class Solution {
public:
    int robRange(vector<int>& nums, int start, int end) {
        int first = nums[start], second = max(nums[start], nums[start + 1]);
        for (int i = start + 2; i <= end; i++) {
            int temp = second;
            second = max(first + nums[i], second);
            first = temp;
        }
        return second;
    }

    int rob(vector<int>& nums) {
        int length = nums.size();
        if (length == 1) {
            return nums[0];
        } else if (length == 2) {
            return max(nums[0], nums[1]);
        }
        return max(robRange(nums, 0, length - 2), robRange(nums, 1, length - 1));
    }
};
```
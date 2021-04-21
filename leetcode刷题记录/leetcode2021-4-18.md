删除有序数组中的重复项

## 双指针

## 引言
* 毕竟这是一道简单题，暴力法是完全可以的，正文开始
## 删除有序数组中的重复项<https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/submissions/>
### 暴力法
* 在这个数组中前后比较，用另一个数组记录不重复的项，然后再copy一下就行了
```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums)
    {
        int length = nums.size();
        if (length == 0) {
            return 0;
        }
        vector<int> v;
        v.push_back(nums[0]);
        for (int i = 0; i < length-1; i++) {
            if (nums[i]!=nums[i+1]) {
                v.push_back(nums[i+1]);
            }
        }
        for (int i = 0; i < v.size(); i++) {
            nums[i] = v[i];
        }
        return v.size();
    }
};
```
### 双指针
* 就是用两个类似于指针的东西在原数组上进行操作，判断对应的项是否重复，再进行指针的加加，还要对项的值进行一下修改，，，
* 时间复杂度：O(n)，其中 n 是数组的长度。快指针和慢指针最多各移动 n 次。
* 空间复杂度：O(1)。只需要使用常数的额外空间。
```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums)
    {
        if (nums.size() == 0) {
            return 0;
        }
        //双指针
        int p = 0, q = 1;
        while (q < nums.size()) {
            if (nums[p]!=nums[q]) {
                nums[p + 1] = nums[q];
                p++;
            }
            q++;
        }
        return p + 1;
    }
};
```
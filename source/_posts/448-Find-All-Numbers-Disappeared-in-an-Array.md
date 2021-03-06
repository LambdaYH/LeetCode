---
title: 448. Find All Numbers Disappeared in an Array
date: 2021-04-12 21:17:46 +0800
categories: leetcode
tags: 
- Array
---
#### [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

##### 抄的discussion

使用原数列中的坐标是否为负来表征当前坐标所代表的值是否存在。由此使得S(n) = O(n)

聪明啊！

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        for(int i = 0; i < nums.size(); ++i)
        {
            int m = abs(nums[i]) - 1;
            nums[m] = nums[m] > 0 ? -nums[m] : nums[m];
        }
        vector<int> ret;
        for(int i = 0; i < nums.size(); ++i)
        {
            if(nums[i] > 0)
                ret.push_back(i + 1);
        }
        return ret;
    }
};
```

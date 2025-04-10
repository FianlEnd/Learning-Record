# **双指针**
***
## **移动0**
```
//一种双指针的运用
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size(), left = 0, right = 0;
        while (right < n) {
            if (nums[right]) {
                swap(nums[left], nums[right]);
                left++;
            }
            right++;
        }
    }
};
```
***
## **三数之和**
[text](https://leetcode.cn/problems/3sum/description)

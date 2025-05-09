# **子串**
***
## **最大子数组和**

```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int pre=0;
        int out=nums[0];
        for(int i=0;i<nums.size();i++)
        {
            pre=max(pre,0)+nums[i];
            out=max(pre,out);
        }
        return out;
    }
};
```
***
## **最大波动子串**

```
class Solution {
public:
    int largestVariance(string s) {
        int ans = 0;
        for (char a = 'a'; a <= 'z'; a++) {
            for (char b = 'a'; b <= 'z'; b++) {
                if (b == a) {
                    continue;
                }
                int f0 = 0, f1 = INT_MIN;
                for (char ch : s) {
                    if (ch == a) {
                        f0 = max(f0, 0) + 1;
                        f1++;
                    } else if (ch == b) {
                        f1 = f0 = max(f0, 0) - 1;
                    } // else f0 = max(f0, 0); 可以留到 ch 等于 a 或者 b 的时候计算，f1 不变
                    ans = max(ans, f1);
                }
            }
        }
        return ans;
    }
};

//优化
class Solution {
public:
    int largestVariance(string s) {
        int ans = 0;
        int f0[26][26]{}, f1[26][26];
        memset(f1, -0x3f, sizeof(f1)); // 初始化成一个很小的负数

        for (char ch : s) {
            ch -= 'a';
            // 遍历到 ch 时，只需计算 a=ch 或者 b=ch 的状态，其他状态和 ch 无关，f 值不变
            for (int i = 0; i < 26; i++) {
                if (i == ch) {
                    continue;
                }
                // 假设出现次数最多的字母 a=ch，更新所有 b=i 的状态
                f0[ch][i] = max(f0[ch][i], 0) + 1;
                f1[ch][i]++;
                // 假设出现次数最少的字母 b=ch，更新所有 a=i 的状态
                f1[i][ch] = f0[i][ch] = max(f0[i][ch], 0) - 1;
                ans = max(ans, max(f1[ch][i], f1[i][ch])); // 或者 max({ans, f1[ch][i], f1[i][ch]})
            }
        }
        return ans;
    }
};
```
***
## **给你一个整数数组 nums 和一个整数 k ，请你统计并返回 该数组中和为 k 的子数组的个数**
```
//子数组是数组中元素的连续非空序列
//两个前缀和之差就是这部分子数组的和
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> s(n + 1);
        for (int i = 0; i < n; i++) {
            s[i + 1] = s[i] + nums[i];
        }

        int ans = 0;
        unordered_map<int, int> cnt;
        for (int sj : s) {
            // 注意不要直接 += cnt[sj-k]，如果 sj-k 不存在，会插入 sj-k
            ans += cnt.contains(sj - k) ? cnt[sj - k] : 0;
            cnt[sj]++;
        }
        return ans;
    }
};
```
***
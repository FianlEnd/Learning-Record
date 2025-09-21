# **堆**
***
## **基于快排的选择排序**
***
```
class Solution {
public:
    int quickselect(vector<int> &nums, int l, int r, int k) {
        if (l == r)
            return nums[k];
        int partition = nums[l], i = l - 1, j = r + 1;
        while (i < j) {
            do i++; while (nums[i] < partition);
            do j--; while (nums[j] > partition);
            if (i < j)
                swap(nums[i], nums[j]);
        }
        if (k <= j)return quickselect(nums, l, j, k);
        else return quickselect(nums, j + 1, r, k);
    }

    int findKthLargest(vector<int> &nums, int k) {
        int n = nums.size();
        return quickselect(nums, 0, n - 1, n - k);
    }
};
```
***
## **前k个高频字母**
***
```
//最小堆...

//桶排序
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // 第一步：统计每个元素的出现次数
        unordered_map<int, int> cnt;
        int max_cnt = 0;
        for (int x : nums) {
            cnt[x]++;
            max_cnt = max(max_cnt, cnt[x]);
        }

        // 第二步：把出现次数相同的元素，放到同一个桶中
        vector<vector<int>> buckets(max_cnt + 1);
        for (auto& [x, c] : cnt) {
            buckets[c].push_back(x);
        }

        // 第三步：倒序遍历 buckets，把出现次数前 k 大的元素加入答案
        vector<int> ans;
        for (int i = max_cnt; i >= 0 && ans.size() < k; i--) {
            ans.insert(ans.end(), buckets[i].begin(), buckets[i].end());
        }
        return ans;
    }
};
```
***
## **2**

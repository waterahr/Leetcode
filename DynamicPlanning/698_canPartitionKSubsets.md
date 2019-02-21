# 698.划分成k个相等的子集

如果可以划分为K个子集,那么每个子集的值肯定是sum/K,依次考察是否可以将nums[i]放入第k个子集中(0<=i<nums.size, 0<=k<K).需要注意的一个问题是,
需要先对数字进行降序排序,如此做可以极大减少回溯的次数.

```cpp
class Solution {
public:
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        int sum = 0, max_num = INT_MIN;
        sort(nums.begin(), nums.end(), greater<int>());
        for(int num:nums){
            sum += num;
            max_num = max(max_num, num);
        }
        if(sum%k || max_num > sum/k)
            return false;
        vector<int> target(k, sum/k);
        return dfs(nums, k, 0, target);
    }
    
private:
    bool dfs(vector<int>& nums, int k, int index, vector<int>& target){
        if(index == nums.size()) return true;
        for(int& t:target)
            if(nums[index] <= t){
                t -= nums[index];
                if(dfs(nums, k, index+1, target)) return true;
                t += nums[index];
            }
        return false;
    }
};
```

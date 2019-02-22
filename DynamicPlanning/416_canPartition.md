# 416.分割等和数组

与[划分成k个相等的子集](https://leetcode-cn.com/problems/partition-to-k-equal-sum-subsets/)相似的思路求解,
参考[c++](./DynamicPlanning/698_canPartitionKSubsets.md).

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for(int num:nums){
            sum += num;
        }
        sort(nums.begin(), nums.end(), greater<int>());
        int max_num = nums[0];
        if(sum%2 || max_num>sum/2)
            return false;
        vector<int> target(2, sum/2);
        return dfs(nums, 0, target);
    }
    
private:
    bool dfs(vector<int>& nums, int index, vector<int>& target){
        if(index == nums.size()) return true;
        for(int& t:target){
            if(nums[index] <= t){
                t -= nums[index];
                if(dfs(nums, index+1, target)) return true;
                t += nums[index];
            }
        }
        return false;
    }
};
```

此外，本题目为典型的背包问题，dp[i]表示数组内是否能够组成一个和为i的子数组,状态转移方程为:
dp[i]=Or{dp[i-nums[j]]}(0<=i<nums.size, nums[j]<=i).

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for(int num:nums){
            sum += num;
        }
        sort(nums.begin(), nums.end(), greater<int>());
        int max_num = nums[0];
        if(sum%2 || max_num>sum/2)
            return false;
        
        vector<bool> dp(sum/2+1, false);
        dp[0] = true;
        for(int i=1; i<=sum/2; i++)
            for(int num:nums)
                if(i >= num){
                    dp[i] = dp[i] || dp[i-num];
                }
        return dp[sum/2];
    }
};
```

不好意思,上面的代码是错误的.上面的代码没有注意到的一个问题就是,每个数字只能放到一个集合中.


```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum = 0;
        for(int num:nums){
            sum += num;
        }
        sort(nums.begin(), nums.end(), greater<int>());
        int max_num = nums[0];
        if(sum%2 || max_num>sum/2)
            return false;
        
        vector<bool> dp(sum/2+1, false);
        dp[0] = true;
        for(int num:nums)
            for(int i=sum/2; i>=num; i--)
                if(i >= num){
                    dp[i] = dp[i] || dp[i-num];
                }
        return dp[sum/2];
    }
};
```

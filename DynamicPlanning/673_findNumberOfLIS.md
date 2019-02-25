# 673.最长递增子序列的个数

dp[i]表示以nums[i]结尾的最长递增子序列的长度,状态转移方程为:dp[i]=max{dp[j]+1}(0<=j<i and nums[j]<nums[i]).

```cpp
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        vector<pair<int, int>> dp(nums.size(), {1, 1});
        int max_len = 1;
        for(int i=1; i<nums.size(); i++){
            for(int j=0; j<i; j++)
                if(nums[j] < nums[i]){
                    if(dp[j].first + 1 > dp[i].first){
                        dp[i].first = dp[j].first + 1;
                        dp[i].second = dp[j].second;
                    }else if(dp[j].first + 1 == dp[i].first)
                        dp[i].second += dp[j].second;
                }
            max_len = max(max_len, dp[i].first);
        }
        int count = 0;
        for(auto p:dp)
            count += (p.first == max_len)?p.second:0;
        return count;
    }
};
```

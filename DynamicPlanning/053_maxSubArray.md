# 53.最大子序和

首先求出前i个数的和，即sum[i-1]=sum[0]+sum[1]+...+sum[i-1];
dp[i]表示以nums[i]结尾的最大子序列和的值,递推关系式为dp[i]=max{dp[i], sum[i]-sum[j]}(j<i).

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max_sum = 0;
        vector<int> sums(nums.size(), 0), dp(nums);
        if(nums.empty()) return max_sum;
        sums[0] = nums[0];
        max_sum = sums[0];
        for(int i=1; i<nums.size(); i++)
            sums[i] = sums[i-1] + nums[i];
        for(int i=0; i<nums.size(); i++){
            dp[i] = sums[i];
            for(int j=0; j<i; j++){
                dp[i] = max(dp[i], sums[i] - sums[j]);
            }
            max_sum = max(max_sum, dp[i]);
        }
        return max_sum;
    }
};
```

题目中要求实现复杂度为O(n)的解法,做法是修改递推关系式，dp[i]表示以nums[i]结尾的最大子序列和的值,则dp[i]与dp[i-1]的正负有关,递推关系式为>=0=>dp[i]=dp[i-1]+nums[i];<0=>dp[i]=nums[i].

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max_sum = 0;
        vector<int> dp(nums);
        if(nums.empty()) return max_sum;
        max_sum = dp[0];
        for(int i=1; i<nums.size(); i++){
            if(dp[i-1]>=0) dp[i]=dp[i-1]+nums[i];
            max_sum = max(dp[i], max_sum);
        }
        return max_sum;
    }
};
```

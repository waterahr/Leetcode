# 377.组合总和Ⅳ

dp[n]表示组合成目标值为n的组合的个数,递推关系式为:dp[n]=Sigma{dp[n-nums[i]]}(0<=i<nums.size).

```cpp
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<double> dp(target+1, 0);
        dp[0] = 1;
        for(int i=1; i<=target; i++){
            for(int& num:nums)
                if(i >= num){
                    dp[i] += dp[i-num];
                }
        }
        return dp[target];
    }
};
```

# 70.爬楼梯

设dp[i]表示爬到i阶的方法数目，递推关系式为:dp[i]=dp[i-1]+dp[i-2]

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp(n+1, 0);
        dp[1] = 1;
        if(n==1) return 1;
        dp[2] = 2;
        for(int i=3; i<=n; i++)
            dp[i] = dp[i-1] + dp[i-2];
        return dp[n];
    }
};
```

# 746.使用最小花费爬楼梯

dp[i]表示到达i阶时的最小花费,递推关系式为dp[i]=min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2])

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        vector<int> dp(cost.size()+1, 0);
        if(cost.size() <= 1) return 0;
        dp[0] = 0;
        dp[1] = 0;
        for(int i=2; i<=cost.size(); i++)
            dp[i] = min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2]);
        return dp[cost.size()];
    }
};
```

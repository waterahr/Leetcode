# 322.零钱兑换

dp[target][i]表示利用coins[:i+1]可以凑成target金额所需的最少硬币数目,状态转移方程为:
dp[target][i]=min{dp[target-coins[i]*j][i-1]+j}(0<=j<=target/coins[i]).

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<vector<int>> dp(amount+1, vector<int>(coins.size(), INT_MAX));
        dp[0][0] = 0;
        for(int j=1; j<=amount; j++)
            if(j%coins[0] == 0) dp[j][0] = j / coins[0];
        for(int i=1; i<coins.size(); i++){
            dp[0][i] = 0;
            for(int j=1; j<=amount; j++)
                for(int k=0; k*coins[i]<=j; k++)
                    if(dp[j-coins[i]*k][i-1]!=INT_MAX)
                        dp[j][i] = min(dp[j][i], dp[j-coins[i]*k][i-1] + k);
        }
        int count = dp[amount][coins.size()-1];
        if(count == INT_MAX) count = -1;
        return count;
    }
};
```

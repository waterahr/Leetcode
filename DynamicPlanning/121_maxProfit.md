# 121.买卖股票的最佳时机

dp[i]表示第i天卖出股票可以得到的最大收益，递推关系式：dp[i] = max{dp[i], dp[j]-prices[j]+prices[i]}(j<=i)

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int max_profit = 0;
        vector<int> dp(prices.size(), 0);
        for(int i=0; i<prices.size(); i++){
            for(int j=0; j<i; j++){
                dp[i] = max(dp[i], dp[j]+prices[i]-prices[j]);
            }
            max_profit = max(max_profit, dp[i]);
        }
        return max_profit;
    }
};
```

还有更直观的做法，只需要一次遍历，即如果当前价格比之前的买入价格更低的话就更新买入价格为当前价格。

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int buy = INT_MAX;
        int profit = 0;
        for (auto p : prices) {
            buy = min (buy, p);
            profit = max(profit, p - buy);
        }
        return profit;
    }
};
```

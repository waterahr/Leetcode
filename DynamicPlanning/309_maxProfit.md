# 309.最佳买卖股票时机含冰冻期

dp_sell[i]表示第i天没有股票买入时可获取的最大收益,dp_buy[i]表示第i天已有股票买入时可获取的最大收益,dp_froze[i]表示第i天处于冰冻期时可获取的最大收益.
递推关系式为:
dp_froze[i]=dp_sell[i-1];
dp_buy[i]=max(dp_froze[i-1]-prices[i], dp_buy[i-1]);
dp_sell[i]=max(prices[i]+dp_buy[i-1], dp_sell[i-1]*, dp_froze[i]*).

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int days = prices.size();
        if(days == 0) return 0;
        vector<int> dp_sell(days, INT_MIN), dp_buy(days, INT_MIN), dp_froze(days, INT_MIN);
        dp_sell[0] = 0;
        dp_buy[0] = -prices[0];
        dp_froze[0] = 0;
        for(int i=1; i<days; i++){
            dp_froze[i] = dp_sell[i-1];
            dp_buy[i] = max(dp_froze[i-1] - prices[i], dp_buy[i-1]);
            dp_sell[i] = max(dp_sell[i-1], dp_buy[i-1] + prices[i]);
        }
        return max(max(dp_sell.back(), dp_buy.back()), dp_froze.back());
    }
};
```

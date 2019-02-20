# 714.买卖股票的最佳时机含手续费

dp_no[i]表示在第i天时没有股票买入时可以获得的最大收益,dp_yes[i]表示在第i天时已有股票买入时可以获得的最大收益.分析可知,
dp_no[i]有两种情况,一是第i-1天已有股票买入而在第i天卖出股票,另是第i-1天没有股票买入而在第i天没有操作;
dp_yes[i]有两种情况,一是第i-1天已有股票买入而在第i天没有操作,另是第i-1天没有股票买入而在第i天买入股票;
故而有递推关系式为:
dp_no[i]=max(dp_yes[i-1]+prices[i]-fee, dp_no[i-1]);
dp_yes[i]=max(dp_yes[i-1], dp_no[i-1]-prices[i]).

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int days = prices.size();
        if(days == 0) return 0;
        vector<int> dp_no(days, INT_MIN), dp_yes(days, INT_MIN);
        dp_no[0] = 0;
        dp_yes[0] = -prices[0];
        for(int i=1; i<days; i++){
            dp_no[i] = max(dp_yes[i-1] + prices[i] - fee, dp_no[i-1]);
            dp_yes[i] = max(dp_yes[i-1], dp_no[i-1] - prices[i]);
        }
        return max(dp_no.back(), dp_yes.back());
    }
};
```

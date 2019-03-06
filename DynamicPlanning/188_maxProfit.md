# 188.买卖股票的最佳时机IV

local[i][j]表示第i天进行了j笔交易,且第j笔是在第i天完成的的最大收益;
global[i][j]表示第i天进行了j笔交易的最大收益,是目前为止全局最优,不规定第j笔在哪天完成.则状态转移方程为:
```
local[i][j]=max(global[i-1][j-1]+max(0, prices[i]-prices[i-1]), local[i-1][j]+prices[i]-prices[i-1])；
global[i][j]=max(local[i][j], global[i-1][j])；
```

```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int len = prices.size();
        if(len == 0) return 0;
        if(k > len) return solveMaxProfit(prices);
        vector<vector<int>> local(len+1, vector<int>(k+1, 0));
        vector<vector<int>> global(len+1, vector<int>(k+1, 0));
        for(int i=2; i<=len; i++){
            int last = prices[i-1] - prices[i-2];
            for(int j=1; j<=k; j++){
                local[i][j] = max(global[i-1][j-1] + max(0, last), local[i-1][j]+last);
                global[i][j] = max(global[i-1][j], local[i][j]);
            }
        }
        return global[len][k];
    }
    
private:
    int solveMaxProfit(vector<int> &prices) {
        int res = 0;
        for (int i = 1; i < prices.size(); ++i) {
            if (prices[i] - prices[i - 1] > 0) {
                res += prices[i] - prices[i - 1];
            }
        }
        return res;
    }
};
```

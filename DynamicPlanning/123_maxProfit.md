# 123.买卖股票的最佳时机III

对于任意一天考虑四个变量:fstBuy-在该天第一次买入股票可获得的最大收益;fstSell-在该天第一次卖出股票可获得的最大收益;
secBuy-在该天第二次买入股票可获得的最大收益;secSell-在该天第二次卖出股票可获得的最大收益.状态转移方程为:
fstBuy=max(fstBuy, -price), fstSell=max(fstSell, price+fstBuy), secBuy=max(secBuy, fstSell - price), secSell=max(secSell, price+secBuy).

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int fstBuy = INT_MIN, fstSell = 0;
        int secBuy = INT_MIN, secSell = 0;
        for(int p : prices) {
            fstBuy = max(fstBuy, -p);
            fstSell = max(fstSell, fstBuy + p);
            secBuy = max(secBuy, fstSell - p);
            secSell = max(secSell, secBuy + p); 
        }
        return secSell;
    }
};
```

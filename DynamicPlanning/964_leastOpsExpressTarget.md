# 964.表示数字的最少运算符

首先要注意审题,没有括号意味着:
- 最后结果一定是x的i次方相加减(i>=0);
- 由于target是整数所以不可能有i<0.
这样的话我们第一反应就是把target转换成x进制,得到:target=Sigma{a[i]\*x^i}.

然后考虑组成每一位时需要的运算符,分为以下两步考虑:

- 组合x^i需要m个运算符,m=i==0?1:i-1;

- 我们需要组合出每个a[i]不为0的a[i]\*x^i,这有两种方法:
  - 用a[i]个x^i相加,此时第i位需要的运算符为a[i]\*(m+1);
  - 用1个x^(i+1)减去x-a[i]个x^i,此时第i位需要的运算符为(x-a[i])\*(m+1),但需要注意的一点是第i+1位需要的数值由a[i+1]\*x^(i+1)变成(a[i+1]+1)\*x^(i+1).

所以,每一位有两种可能性,一种是要组合a[i],另一种是要组合a[i+1],我们令dp[i][0]和dp[i][1]表示第i位组合a[i]和a[i+1]时的最小运算符数,状态转移方程为:
```
dp[i][0]=min{dp[i+1][0]+a[i]\*(m+1), dp[i+1][1]+(x-a[i])\*(m+1)};

dp[i][1]=min{dp[i+1][0]+(a[i]+1)\*(m+1), dp[i+1][1]+(x-a[i]-1)\*(m+1)}.
```

```cpp
class Solution {
public:
    int leastOpsExpressTarget(int x, int target) {
        vector<int> res;
        while (target){
            res.push_back(target % x);
            target /= x;
        }
        int n = res.size();
        int last[2] = {0, n};
        for(int i=n-1; i>=0; i--){
            int m = i;
            if(!i) m = 2;
            int tmp[2] = {last[0], last[1]};
            last[0] = min(tmp[1] + (x - res[i]) * m, tmp[0] + res[i] * m);
            last[1] = min(tmp[1] + (x - res[i] - 1) * m, tmp[0] + (res[i] + 1) * m);
        }
        return last[0]-1;
    }
};
```

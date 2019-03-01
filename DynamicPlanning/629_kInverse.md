# 629.k个逆序对数组

假如当前的4个数字的排列方式为:xxxx,再往其中添加一个数字5有如下几种添加方式：
- xxxx5:多出0个逆序对,因此有f1(5,k)=f(4,k)
- xxx5x:多出1个逆序对,因此有f2(5,k+1)=f(4,k)=>f2(5,k)=f(4,k-1)
- xx5xx:多出2个逆序对,因此有f3(5,k+2)=f(4,k)=>f3(5,k)=f(4,k-2)
- x5xxx:多出3个逆序对,因此有f4(5,k+3)=f(4,k)=>f4(5,k)=f(4,k-3)
- 5xxxx:多出4个逆序对,因此有f5(5,k+4)=f(4,k)=>f5(5,k)=f(4,k-4)
=>
f(5,k) = f1 + f2 + f3 + ... + f5
=>
f(5,k) = f(4,k) + f(4,k-1) + f(4,k-2) + f(4,k-3) + f(4,k-5+1)
=>
f(n,k) = f(n-1,k)+f(n-1,k-1) + f(n-1,k-2) + f(n-1,k-3) + ... + f(n-1,k-n+1)
=>
f(n,k+1) = f(n-1,k+1) + f(n-1,k) + f(n-1,k-1) + ... + f(n-1,k-n+2)
=>
f(n,k+1) - f(n,k) = f(n-1,k+1) - f(n-1,k-n+1)
=>
f(n,k+1) = f(n,k) + f(n-1,k+1) - f(n-1,k-n+1)
=>
f(n,k) = f(n,k-1) + f(n-1,k) - f(n-1,k-n).

```cpp
class Solution {
public:
    int kInversePairs(int n, int k) {
        int M = pow(10, 9)+7;
        vector<vector<int>> dp(n+1, vector<int>(k+1, 0));
        for(int i=1; i<=n; i++)
            dp[i][0] = 1;
        for(int i=2; i<=n; i++)
            for(int j=1; j<=k; j++){
                dp[i][j] = (dp[i][j-1] + dp[i-1][j]) % M;
                if(j-i >= 0)
                    dp[i][j] = (dp[i][j] - dp[i-1][j-i]) % M;
                if(dp[i][j] < 0) dp[i][j] += M;
            }
        return dp[n][k];
    }
};
```

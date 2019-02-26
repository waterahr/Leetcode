# 837.新21点

题目的意思是,在已有点数不超过K的情况下,可以从[1, W]中任选一个数,保证和不超过N.求最后当点数超过K时,这个点数小于N的概率.
这个问题其实类似于爬楼梯,每次可跨上[1, W]阶楼梯.
采用动态规划,dp[i]表示点数为i的概率,只有当已有点数小于K时,才能再取数,所以有:
(1)当i<=K时,dp[i]=(前W个dp之和)/W; 
(2)当K<i<K+W时,前一次最多只能是K-1点,最少为i-W点,所以dp[i]=(dp[K-1]+dp[K-2]+…+dp[i-W])/W; 
(3)当i>=K+W时,无论如何都无法取到,dp[i]=0.

```cpp
class Solution {
public:
    double new21Game(int N, int K, int W) {
        vector<double> dp(N+1, 0);
        double prob = 0;
        double sum_prob = 1.0;
        for(int i=1; i<=N; i++){
            dp[i] = sum_prob / W;
            //当i>=K时，不能再取数，因此后面的概率不能累加
            if(i<K) sum_prob += dp[i];
            //因为只需要计算前w个dp之和，所以当i>=W时，减去最前面的dp
            if(i-W >= 0 && i-W < K) sum_prob -= dp[i - W];
            if(i >= K) prob += dp[i];
        }
        return prob;
    }
};
```

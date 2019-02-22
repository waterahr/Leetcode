# 813.最大平均值和的分组

dp[k][i]表示数组nums[:i]划分为k个非空子数组的最大平均值和,递推关系式为:
dp[k][i]=max{dp[k-1][j]+sum(nums[j:i])/(i-j)}(1<=j<=i-1).

```cpp
class Solution {
public:
    double largestSumOfAverages(vector<int>& A, int K) {
        vector<vector<double>> dp(K+1, vector<double>(A.size()+1, 0));
        for(int i=0; i<A.size(); i++)
            dp[1][i+1] = (dp[1][i] * i + A[i]) / ( i + 1);
        for(int k=2; k<=K; k++)
            for(int i=1; i<=A.size(); i++)
                for(int j=1; j<i; j++)
                    dp[k][i] = max(dp[k][i], dp[k-1][j] + (dp[1][i] * i - dp[1][j] * j) / (i - j));
        //cout<<k<<' '<<i<<"->"<<dp[k][i]<<endl;
        return dp[K][A.size()];
    }
};
```

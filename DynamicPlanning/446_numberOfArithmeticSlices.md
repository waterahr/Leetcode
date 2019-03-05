# 446.等差数列划分II - 子序列

dp[i][j]表示以nums[i], nums[j]结尾的等差数列的个数, 状态转移方程为:
```
dp[i][j]=Sigma{dp[k][i]}(nums[j]+nums[k]==2*nums[i]).
```

```cpp
class Solution {
public:
    int numberOfArithmeticSlices(vector<int>& A) {
        int len = A.size();
        vector<vector<int>> dp(len, vector<int>(len, 0));
        int count = 0;
        for(int j=2; j<len; j++)
            for(int i=1; i<j; i++){
                for(int k=0; k<i; k++){
                    long tmp1 = (long)A[i] + A[i], tmp2 = (long)A[j] + A[k];
                    if(tmp1 == tmp2){
                        dp[i][j] += dp[k][i] + 1;
                    }
                }
                count += dp[i][j];
            }
        return count;
    }
};
```

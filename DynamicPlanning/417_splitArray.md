# 417.分割数组的最大值

dp[i][j]表示将子数组nums[:j]分成i个分组的各组中的最大值和的最小值,状态转移方程为:
dp[i][j]=min{max(dp[i-1][k], sum(nums[k:j))}.

```cpp
class Solution {
public:
    int splitArray(vector<int>& nums, int m) {
        int length = nums.size();
        vector<vector<long>> dp(m+1, vector<long>(length+1, INT_MAX));
        dp[0][0] = 0;
        vector<long> sums(length+1, 0);
        for (int i=1; i<=length; i++)
            sums[i] = sums[i-1] + nums[i-1];
        for(int i=1; i<=m; i++)
            for(int j=1; j<=length; j++)
                for(int k=i-1; k<j; k++){
                    long val = max(dp[i-1][k], sums[j]-sums[k]);
                    dp[i][j] = min(dp[i][j], val);
                }
        return dp[m][length];
    }
};
```

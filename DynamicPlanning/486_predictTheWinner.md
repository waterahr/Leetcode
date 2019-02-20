# 486.预测赢家

dp[i][j]表示区间[i, j]内的数组先手可多拿取的分数,递推关系式为:
dp[i][j]=max(nums[i]-dp[i+1][j], nums[j]-dp[i][j-1]).

```cpp
class Solution {
public:
    bool PredictTheWinner(vector<int>& nums) {
        int len = nums.size();
        vector<vector<int>> dp(len, vector<int>(len, 0));
        for(int i=0; i<len; i++)
            dp[i][i] = nums[i];
        for(int i=len-1; i>=0; i--)
            for(int j=i+1; j<len; j++)
                dp[i][j] = max(nums[i] - dp[i+1][j], nums[j] - dp[i][j-1]);
        return dp[0][len-1] >= 0;
    }
};
```

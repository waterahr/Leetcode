# 474.一和零

遍历所有的字符串,当遍历到第k个字符串时,dp[i][j]表示用i个1和j个0可以组成的strs[:k+1]中的字符串的最多个数,递推关系式为:
dp[i][j]=max{dp[i][j], dp[i-ones(strs[k])][j-zeros(strs[k])]+1}(n>=i>=ones(strs[k]), m>=j>=zeros(strs[k])).

```cpp
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));
        for (string str : strs) {
            int zeros = 0, ones = 0;
            for (char c : str) (c == '0') ? ++zeros : ++ones;
            for (int i = n; i >= ones; i--)
                for (int j = m; j >= zeros; j--)
                    dp[i][j] = max(dp[i][j], dp[i - ones][j - zeros] + 1);
        }
        return dp[n][m];
    }
};
```

需要注意的是,i,j的遍历必须是递减的.Array = {"10", "0001", "111001", "1", "0"}, m = 5, n = 3的例子中,以遍历到"10"为例,若递增计算的话,dp[1][1]=dp[1][2]=...=dp[2][1]=1;dp[2][2]=max(dp[2][2], dp[1][1]+1)=2(组成了2个"10"，实际上应该是1).

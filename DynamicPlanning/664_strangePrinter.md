# 664.奇怪的打印机

dp[i][j]表示打印s[i:j+1]需要的最少操作数,状态转移方程为:
```
dp[i][j]=min{dp[i][k]+dp[k+1][j-1]}(s[k]==s[j], i<k<j).
```

```cpp
class Solution {
public:
    int strangePrinter(string s) {
        int n = s.length();
        vector<vector<int>> dp(n, vector<int>(n, 0));
        return dfs(s, 0, n-1, dp);
    }
    
private:
    int dfs(string& s, int l, int r, vector<vector<int>>& dp){
        if(l > r) return 0;
        if(dp[l][r]) return dp[l][r];
        dp[l][r] = dfs(s, l, r-1, dp) + 1;
        for(int i=l; i<r; i++)
            if(s[i] == s[r])
                dp[l][r] = min(dp[l][r], dfs(s, l, i, dp) + dfs(s, i+1, r-1, dp));
        return dp[l][r];
    }
};
```

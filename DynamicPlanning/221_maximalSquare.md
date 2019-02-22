# 221.最大正方形

dp[i][j]表示以坐标为(i-1, j-1)位置为右下角所能构成的最大正方形边长, 则递推式为:dp[i][j]=1+min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1])(matrix[i-1][j-1]==1).

```cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int m = matrix.size();
        if(m == 0) return 0;
        int n = matrix[0].size();
        if(n == 0) return 0;
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        int max_len = 0;
        for(int i=1; i<=m; i++)
            for(int j=1; j<=n; j++)
                if(matrix[i-1][j-1]=='1'){
                    dp[i][j] = min(min(dp[i][j-1], dp[i-1][j]), dp[i-1][j-1]) + 1;
                    //cout<<i<<' '<<j<<"->"<<dp[i][j]<<endl;
                    max_len = max(max_len, dp[i][j]);
                }
        return max_len * max_len;
    }
};
```

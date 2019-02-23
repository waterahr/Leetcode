# 62.不同路径

设dp[i][j]表示到达坐标(i, j)位置的不同路径个数,递推关系式为:dp[i][j]=dp[i-1][j]+dp[i][j-1].

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        dp[0][1] = 1;
        for(int i=1; i<=m; i++)
            for(int j=1; j<=n; j++)
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
        return dp[m][n];
    }
};
```

另一个简单做法是,计算走到终点处,共需要向右移动n-1次、向下移动m-1次,问题转换为求解n-1个右以及m-1个下的全排列.

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        int total = m + n - 2, one_direc = min(m-1, n-1);
        long count = 1;
        for(int i=1; i<=one_direc; i++, total--)
            count *= total;
        for(; one_direc>1; one_direc--)
            count /= one_direc;
        return count;
    }
};
```

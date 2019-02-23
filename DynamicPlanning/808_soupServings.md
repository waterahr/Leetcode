# 808.分汤

直觉告诉我们，当N趋向于无穷大时,A先被serve完以及A和B同时被serve完的概率会无限接近于1.经过严格计算我们知道当N >= 4800之后,返回的概率值与1的差距就小于10^6了.所以当N >= 4800的时候,我们就直接返回1.dp[i][j]表示仍然有i毫升A和j毫升B的概率,递推关系式为:dp[i][j]=0.25*(dp[i+100][j]+dp[i+75][j+25]+dp[i+50][j+50]+dp[i+25][j+75]).

```cpp
class Solution {
public:
    double soupServings(int N) {
        if(N>=4800)
        	return 1.0;
        int n = N / 25;
        if(N%25 != 0) n++;
        N = n;
        vector<vector<vector<double>>> dp(N+1, vector<vector<double>>(N+1, vector<double>(N+1, 0)));
        vector<pair<int, int>> opt{{4, 0}, {3, 1}, {2, 2}, {1, 3}};;
        dp[0][N][N] = 1;
        for(int m=1; m<=N; m++)
            for(int i=N; i>=0; i--)
                for(int j=N; j>=0; j--)
                    for(int k=0; k<4; k++){
                        int a = i + opt[k].first, b = j + opt[k].second;
                        if(a>N && i==0) a = N;
                        if(b>N && j==0) b = N;
                        if(a<=N && b<=N) dp[m][i][j] += 0.25 * dp[m-1][a][b];
                    }
        double first_prob = 0, together_prob = 0;
        for(int m=0; m<=N; m++){
            together_prob += dp[m][0][0];
            for(int j=1; j<=N; j++)
                first_prob += dp[m][0][j];
            }
        return first_prob + together_prob / 2;
    }
};
```

上面的代码个人认为一直没有找到错误的原因,先撂在这里等以后有时间再好好研究一下吧...利用递归直接模拟分汤的过程即可求得结果,
dp[i][j]表示仍然有i毫升A和j毫升B的概率计算结果,此时的递推关系式为:
dp[i][j]=0.25*(dp[i-100][j]+dp[i-75][j-25]+dp[i-50][j-50]+dp[i-25][j-75]).


```cpp
class Solution {
public:
    double soupServings(int N) {
        if(N>=4800)
        	return 1.0;
        vector<vector<double>> dp(N+1, vector<double>(N+1, -1));
        return dfs(N, N, dp);
    }
    
private:
    double dfs(int A, int B, vector<vector<double>>& dp){
        if(A <= 0 && B > 0) return 1;
        if(A <= 0 && B <= 0) return 0.5;
        if(A > 0 && B <= 0) return 0;
        if(dp[A][B] > 0) return dp[A][B];
        double prob = 0.25 * (dfs(A - 100, B, dp) + dfs(A - 75, B - 25, dp)
                       + dfs(A - 50, B - 50, dp) + dfs(A - 25, B - 75, dp));
        dp[A][B] = prob;
        return prob;
    }
};
```


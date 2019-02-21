# 688."马"在棋盘上的概率

dp[k][i][j]表示在坐标为(i, j)位置处时走了k步棋子依然在棋盘上的概率,递推关系式为:dp[k][i][j]=Sigma{dp[k-1][x][y]}/8(x,y为下一步可能在的位置).

```cpp
class Solution {
public:
    double knightProbability(int N, int K, int r, int c) {
        vector<vector<vector<double>>> dp(K+1, vector<vector<double>>(N, vector<double>(N, 0)));
        dp[0][r][c] = 1;
        vector<pair<int, int>> step{{1,-2},{1,2},{-1,-2},{-1,2},{2,1},{2,-1},{-2,1},{-2,-1}};
        for(int k=1; k<=K; k++)
            for(int i=0; i<N; i++)
                for(int j=0; j<N; j++)
                    for(auto s:step){
                        int x = i + s.first, y = j + s.second;
                        if(x>=0 && y>=0 && x<N && y<N)
                            dp[k][i][j] += 0.125 * dp[k-1][x][y];
                    }
        double prob = 0;
        for(int i=0; i<N; i++)
            for(int j=0; j<N; j++)
                prob += dp[K][i][j];
        return prob;
    }
};
```

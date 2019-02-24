# 787.K站中转内最便宜航班

dp[k][i][j]表示k站中转时从i到j的最便宜航班,状态转移方程为:dp[k][i][j]=min{dp[k-1][i][flight[0]]+flight[2]}(flight[1]==j for flight in flights).

```cpp
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int K) {
        vector<vector<vector<int>>> dp(K+1, vector<vector<int>>(n, vector<int>(n, INT_MAX)));
        for(auto flight:flights)
            dp[0][flight[0]][flight[1]] = flight[2];
        int min_cost = dp[0][src][dst];
        for(int k=1; k<=K; k++)
            for(int i=0; i<n; i++)
                for(int j=0; j<n; j++){
                    for(auto flight:flights)
                        if(flight[1] == j && dp[k-1][i][flight[0]] != INT_MAX){
                            dp[k][i][j] = min(dp[k][i][j], dp[k-1][i][flight[0]] + flight[2]);
                        }
                    min_cost = min(min_cost, dp[k][src][dst]);
                }
        if(min_cost == INT_MAX) min_cost = -1;
        return min_cost;
    }
};
```

妈耶！一写发现是四重循环,虽然知道肯定超时i,但是还是记录一下.主要是需要精炼状态转移方程,dp[k][i]表示至多经过k次中转机可以达到目的地i的最便宜航班,状态转移方程为:dp[k][i]=min{dp[k-1][i], dp[k-1][flight[0]]+flight[2]}(i==flight[1] for flight in flights).

```cpp
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int K) {
        vector<vector<int>> dp(K+1, vector<int>(n, INT_MAX));
        dp[0][src] = 0;
        for(auto flight:flights)
            if(src == flight[0]) dp[0][flight[1]] = flight[2];
        for(int k=1; k<=K; k++)
            for(auto flight:flights){
                dp[k][flight[1]] = min(dp[k][flight[1]], dp[k-1][flight[1]]);
                if(dp[k-1][flight[0]] != INT_MAX)
                    dp[k][flight[1]] = min(dp[k][flight[1]], dp[k-1][flight[0]] + flight[2]);
            }
        if(dp[K][dst] == INT_MAX) dp[K][dst] = -1;
        return dp[K][dst];
    }
};
```

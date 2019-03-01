# 847.访问所有节点的最短路径

```cpp
class Solution {
public:
    int dp[1<<12][12];
    int dis[12][12] ; 
    void floyd( vector< vector< int> > & graph ){
        int n = graph.size(); 
        { //floyd algorithm
        //   init floyd algorithm
        for( int i =0 ; i < n; i++){
            for( int j =0 ; j<n ; j++){
                dis[i][j] = n*n ; 
            }
        }
        for( int i  =0 ; i< n; i ++){
            dis[i][i] = 0 ; 
        }
        for( int u = 0 ; u<n ; u++){
            for( auto & v : graph[u] ){
                dis[u][v] = 1 ;
                dis[v][u] = 1; 
            }
        }
        // get the table of dis[i][j] 
            for( int k =0 ; k< n ;k++){
                for( int i =0 ; i<n ; i++){
                    for( int j=0 ; j<n ; j++){
                        if( k!=i && k!=j ){
                            dis[i][j] = min( dis[i][j] , dis[i][k] +dis[k][j] ) ; 
                        }
                    }
                }
            }
        }
    }
    int shortestPathLength(vector<vector<int>>& graph) {
        int n = graph.size() ; 
        floyd( graph ) ; 
        // init  dp array ;
        for( int i=0 ; i< n ; i++){
            for( int j=0 ; j<( 1<<n ) ; j++){
                dp[j][i] = n*n; 
            }
        }
        for( int i=0 ; i< n; i++){
            dp[1<<i][i] = 0 ; 
        }
        for( int j=1 ; j<(1<<n) ;  j++){
            for(int i=0;i<n ;i++){
                if( j &(1<<i) ) { // now the ith vertex is actually in the Set j 
                    for( int k=0 ;k<n ;k++){
                        dp[j][i] = min( dp[j][i] , dp[j^(1<<i)][k]+dis[k][i] ) ; 
                    }
                }
            }
        }
        int res = 1<< 15 ; 
        for( int i=0 ; i< n; i++){
            res = min ( res , dp[(1<<n) -1][i] ) ; 
        }
        return res; 
    }
};
--------------------- 
作者：玉界尺 
来源：CSDN 
原文：https://blog.csdn.net/weixin_38739799/article/details/80596691 
版权声明：本文为博主原创文章，转载请附上博文链接！
```
--------------------- 
作者：玉界尺 
来源：CSDN 
原文：https://blog.csdn.net/weixin_38739799/article/details/80596691 
版权声明：本文为博主原创文章，转载请附上博文链接！

# 718.最长重复子数组

dp[i][j]表示数组A[:i]与数组B[:j]的最长重复子数组的长度,递推关系式为:dp[i][j]=max(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]+1(only A[i-1]==B[j-1])).

```cpp
class Solution {
public:
    int findLength(vector<int>& A, vector<int>& B) {
        vector<vector<int>> dp(A.size()+1, vector<int>(B.size()+1, 0));
        if(A.size() == 0 || B.size() == 0)
            return 0;
        for(int i=1; i<=A.size(); i++)
            for(int j=1; j<=B.size(); j++){
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
                if(A[i-1] == B[j-1])
                    dp[i][j] = max(dp[i][j], dp[i-1][j-1] + 1);
            }
        return dp[A.size()][B.size()];
    }
};
```

原来递推关系式写错了,上面的程序求得的结果是两个数组的最长重复不连续子数组.对于连续的最长重复子数组,dp[i][j]表示以A[i-1]、B[j-1]结尾的最长重复子数组的长度,
递推关系式为:dp[i][j]=dp[i-1][j-1]+1.

```cpp
class Solution {
public:
    int findLength(vector<int>& A, vector<int>& B) {
        vector<vector<int>> dp(A.size()+1, vector<int>(B.size()+1, 0));
        if(A.size() == 0 || B.size() == 0)
            return 0;
        int max_len = 0;
        for(int i=1; i<=A.size(); i++)
            for(int j=1; j<=B.size(); j++){
                if(A[i-1] == B[j-1])
                    dp[i][j] = dp[i-1][j-1] + 1;
                max_len = max(max_len, dp[i][j]);
            }
        return max_len;
    }
};
```

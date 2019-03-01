# 730.统计不同回文子字符串的个数

dp[i][j]表示字符串s[i:j+1]的不同回文子字符串的个数,状态转移方程为:
```
dp[i][j]=(s[i]==s[j])?dp[i+1][j]+dp[i][j-1]+1:dp[i+1][j]+dp[i][j-1]-dp[i+1][j-1];
```
需要注意的是,上面的状态转移方程并没有考虑题目中所说的相同字母的下标不同时被视作不同的子字符串,故状态转移方程还需要添加:
```
dp[i][j]+=dp[k][j](i<k<j, s[k]==s[i]) 
```

```cpp
class Solution {
public:
    int countPalindromicSubsequences(string S) {
        vector<vector<int>> dp(S.length(), vector<int>(S.length(), 0));
        for(int i=0; i<S.length(); i++)
            dp[i][i] = 1;
        for(int i=S.length()-1; i>=0; i--)
            for(int j=i+1; j<S.length(); j++){
                if(S[i] == S[j])
                    dp[i][j] = (dp[i+1][j] + dp[i][j-1] + 1) % 1000000007;
                else 
                    dp[i][j] = (dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1]) % 1000000007;
                for(int k=i+1; k<j; k++)
                    if(S[k] == S[i])
                        dp[i][j] = (dp[i][j] + dp[k][j] - dp[k+1][j] - 1) % 1000000007;
            }
        return dp[0][S.length()-1];
    }
};
```

原来我理解错误题意了,相同的仅记一次.在s[i]==s[j]情况下,分为三种情况:1. s[i+1~j-1]之间不含有字母s[i];2. 含有1个字母s[i];3. 含有>=2个字母s[i].
DP的递推过程如下图：
![](https://img-blog.csdn.net/20171128212741262?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGlsaTA3MTA0MzI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![](https://img-blog.csdn.net/20171128212604730?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGlsaTA3MTA0MzI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```cpp
class Solution {
public:
    int countPalindromicSubsequences(string S) {
        int n = S.size();
        if(n == 0) return 0;
        long int M = 1000000007;
        vector<vector<int>> dp(n, vector<int>(n, 0));
        for(int i=0; i<n; i++)
            dp[i][i]=1;
        
        for(int len=1; len<n; len++){
            for(int i=0; i<n-len; i++){
                int j = i+len;
                if(S[i] == S[j]){
                    dp[i][j] = dp[i+1][j-1]*2;
                    int l = i+1;
                    int r = j-1;
                    while(l<=r && S[l]!=S[i]) l++;
                    while(l<=r && S[r]!=S[i]) r--;
                    if(l == r){
                        dp[i][j] += 1;
                    }else if(l < r){
                        dp[i][j] -= dp[l+1][r-1];
                    }else{
                        dp[i][j] += 2;
                    }
                }else{
                    dp[i][j] = dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1];
                }
                dp[i][j]=(dp[i][j] + M) % M;
            }
        }
        return dp[0][n-1];
    }
};
```

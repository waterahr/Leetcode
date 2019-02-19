# 712.两个字符串的最小ASCII删除和

问题转换成寻找两个字符串的最大ASCII和的相等子串(删除若干字符后剩余字符按照顺序组成的字符串),dp[i][j]表示s1[:i+1]与s2[:j+1]的相等子串的最大ASCII和,
递推关系式为:s1[i]==s2[j]=>dp[i][j]=dp[i-1][j-1]+ord(s1[i]);s1[i]!=s2[j]=>dp[i][j]=max(dp[i-1][j], dp[i][j-1]).

```cpp
class Solution {
public:
    int minimumDeleteSum(string s1, string s2) {
        int len1 = s1.length(), len2 = s2.length();
        vector<vector<int>> dp(len1, vector<int>(len2, 0));
        int total = 0;
        for(int i=0; i<len1; i++){
            total += ord(s1[i]);
            for(int j=0; j<len2; j++){
                if(s1[i] == s2[j]){
                    if(i==0 || j==0) dp[i][j] = ord(s1[i]);
                    else dp[i][j] = dp[i-1][j-1] + ord(s1[i]);
                }else{
                    if(i==0 && j!=0) dp[i][j] = dp[i][j-1];
                    else if(i==0 && j==0) dp[i][j] = 0;
                    else if(i!=0 && j==0) dp[i][j] = dp[i-1][j];
                    else dp[i][j] = max(dp[i][j-1], dp[i-1][j]);
                }
                if(i==0) total += ord(s2[j]);
            }
        }
        return total - dp[len1-1][len2-1] * 2;
    }
    
private:
    int ord(char c){
        return 0+c;
    }
};
```

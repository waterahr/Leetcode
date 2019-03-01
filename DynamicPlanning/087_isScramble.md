# 87.扰乱字符串

判断s1和s2是否是扰乱字符串,s1和s2必须长度相等、所包含的元素相同,
在1～s1.length()-1之间存在一个长度i,将s1和s2划分成两个子字符串,这两个子字符串也应互为扰乱字符串,符合条件返回true,否则返回false.

```cpp
class Solution {
public:
    bool isScramble(string s1, string s2) {
        if(s1.length() != s2.length()) 
            return false;
        if(s1 == s2) return true;
        int count[26] = {0};
        for(int i=0; i<s1.length(); i++){
            count[s1[i] - 'a']++;
            count[s2[i] - 'a']--;
        }
        for(int i=0; i<26; i++)
            if(count[i]!=0) 
                return false;
        for(int i=1; i<s1.length(); i++){
            string left1 = s1.substr(0, i), right1 = s1.substr(i);
            string left2 = s2.substr(0, i), right2 = s2.substr(i);
            if(isScramble(left1, left2) && isScramble(right1, right2))
                return true;
            left2 = s2.substr(s1.length()-i);
            right2 = s2.substr(0, s1.length()-i);
            if(isScramble(left1, left2) && isScramble(right1, right2))
                return true;
        }
        return false;
    }
};
```

dp[len][i][j]表示s1[i:i+len]与s2[j:j+len]是否为扰乱字符串,解决思路与上面的代码相同,状态转移方程为:
dp[len][i][j]=Or{(dp[k][i][j]&&dp[len-k][i+len][j+len]) || (dp[k][i][j+len-k]&&dp[len-k][i+len][j])}.

```cpp
class Solution {
public:
    bool isScramble(string s1, string s2) {
        int len1=s1.length(), len2=s2.length();
        vector<vector<vector<bool>>> dp(len1, vector<vector<bool>>(len1, vector<bool>(len1, false)));
        if(len1 != len2)
            return false;
        for(int i=0;i<len1;i++)
            for(int j=0;j<len1;j++)
                if(s1[i] == s2[j])
                    dp[0][i][j] = true;
        for(int k=1;k<len1;k++)
            for(int i=0;i<len1-k;i++)
                for(int j=0;j<len1-k;j++)
                    if(false == dp[k][i][j])
                        for(int q=0; q<k; q++)
                            if( (dp[q][i][j] && dp[k-q-1][i+q+1][j+q+1]) || (dp[q][i][j+k-q] && dp[k-q-1][i+q+1][j]) )
                                dp[k][i][j] = true;
 
        return dp[len1-1][0][0];
    }
};
```

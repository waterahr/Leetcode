# 873.最长的斐波那契子序列的长度

dp[i]表示以nums[i]结尾的最长斐波那契子序列的长度,因为判断是否构成斐波那契序列需要计算该数字前面的两个数,故用pre[i]保存前一个数.
递推关系式为:对于0<=j<i,nums[i]==pre[j]+nums[j]?dp[i]=max(dp[i], dp[j]+1),pre[i]=nums[j](与dp[i]同时更新):dp[i].

```cpp
class Solution {
public:
    int lenLongestFibSubseq(vector<int>& A) {
        vector<int> dp(A.size(), 2);
        vector<unordered_set<int>> pre(A.size());
        dp[0] = 1;
        dp[1] = 2;
        pre[1].insert(A[0]);
        int max_len = 0;
        for(int i=2; i<A.size(); i++){
            unordered_set<int> dict;
            for(int j=0; j<i; j++){
                if(dict.find(A[i] - A[j]) != dict.end()){
                    if(dp[i] < 3){
                        dp[i] = 3;
                        pre[i].clear();
                        pre[i].insert(A[j]);
                    }else if(dp[i] == 3)
                        pre[i].insert(A[j]);
                }
                dict.insert(A[j]);
                for(int p:pre[j]){
                    if(A[i] == A[j]+p){
                        int cur_len = dp[j] + 1;
                        if(cur_len > dp[i]){
                            pre[i].clear();
                            pre[i].insert(A[j]);
                            dp[i] = cur_len;
                        }else if(cur_len == dp[i])
                            pre[i].insert(A[j]);
                    }
                }
            }
            max_len = max(max_len, dp[i]);
        }
        if(max_len < 3) max_len = 0;
        return max_len;
    }
};
```

上面的方法不能顺利通过所有测试用例,分析可知,上面的思路已经有贪心的思路在里面,也就是中间有些结果已经被更新删除了,
然而此题目中局部最优的结果并不一定能够得到全局最优.

重新定义,dp[i][j]表示以A[i]和B[j]结尾的最长斐波那契子序列的长度,递推关系式为:
dp[i][j]=max{dp[i][j], dp[k][i]+1}(0<=k<i, nums[k]+nums[i]=nums[j]).

```cpp
class Solution {
public:
    int lenLongestFibSubseq(vector<int>& A) {
        vector<vector<int>> dp(A.size(), vector<int>(A.size(), 2));
        /*for(int i=0; i<A.size(); i++){
            dp[i][i] = 1;
        }*/
        int max_len = 0;
        for(int j=0; j<A.size(); j++)
            for(int i=0; i<j; i++){
                for(int k=0; k<i; k++)
                    if(A[k] + A[i] == A[j])
                        dp[i][j] = max(dp[i][j], dp[k][i]+1);
                max_len = max(max_len, dp[i][j]);
            }
        if(max_len < 3) max_len = 0;
        return max_len;
    }
};
```

超出时间限制,对代码进行优化,将内层的两个for循环利用双指针可以提高时间效率.

```cpp
class Solution {
public:
    int lenLongestFibSubseq(vector<int>& A) {
        vector<vector<int>> dp(A.size(), vector<int>(A.size(), 2));
        /*for(int i=0; i<A.size(); i++){
            dp[i][i] = 1;
        }*/
        int max_len = 0;
        for(int j=0; j<A.size(); j++){
            int l = 0, r = j-1;
            while(l < r){
                int sum = A[l] + A[r];
                if(sum == A[j]){
                    dp[r][j] = max(dp[r][j], dp[l][r]+1);
                    max_len = max(max_len, dp[r][j]);
                    l++;
                    r--;
                }else if(sum < A[j])
                    l++;
                else
                    r--;
            }
        }
        
        if(max_len < 3) max_len = 0;
        return max_len;
    }
};
```

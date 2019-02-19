# 413.等差数列划分

设dp[i]表示以num[i]结尾的等差数列的个数,因为数列必须是数组中的一个连续子数组,所以dp[i]要么是0,要么有递推关系式为:dp[i]=1+dp[i-1].

```cpp
class Solution {
public:
    int numberOfArithmeticSlices(vector<int>& A) {
        vector<int> dp(A.size(), 0);
        int number = 0;
        if(A.size() <= 2) return 0;
        for(int i=2; i<A.size(); i++)
            if(A[i] - A[i-1] == A[i-1] - A[i-2]){
                dp[i] = 1 + dp[i-1];
                number += dp[i];
            }
        return number;
    }
};
```

# 801.使序列递增的最小交换次数

dp_swap[i]表示交换A[i]与B[j]使序列递增的最小交换次数,dp_keep[i]表示不交换A[i]与B[j]使序列递增的最小交换次数.状态转移方程为:
A[i]>A[i-1]&&B[i]>B[i-1]?dp_swap[i]=min(dp_swap[i], dp_swap[i-1]+1),dp_keep[i]=min(dp_keep[i], dp_keep[i-1]);
A[i]>B[i-1]&&B[i]>A[i-1]?dp_swap[i]=min(dp_swap[i], dp_keep[i-1]+1),dp_keep[i]=min(dp_keep[i], dp_swap[i-1]).

```cpp
class Solution {
public:
    int minSwap(vector<int>& A, vector<int>& B) {
        vector<int> dp_swap(A.size(), INT_MAX), dp_keep(dp_swap);
        dp_swap[0] = 1;
        dp_keep[0] = 0;
        for(int i=1; i<A.size(); i++){
            if(A[i] > A[i-1] && B[i] > B[i-1]){
                dp_keep[i] = min(dp_keep[i], dp_keep[i-1]);
                dp_swap[i] = min(dp_swap[i], dp_swap[i-1]+1);
            }
            if(A[i] > B[i-1] && B[i] > A[i-1]){
                dp_keep[i] = min(dp_keep[i], dp_swap[i-1]);
                dp_swap[i] = min(dp_swap[i], dp_keep[i-1]+1);
            }
        }
        return min(dp_swap.back(), dp_keep.back());
    }
};
```

# 517.超级洗衣机

```cpp
class Solution {
public:
    int findMinMoves(vector<int>& machines) {
        int length = machines.size();
        vector<int> sum(length, 0);
        if(length<=1)
            return 0;
        sum[0] = machines[0];
        for(int i=1;i<length;i++)
            sum[i] = sum[i-1] + machines[i];
        if(sum[length-1]%length)
            return -1;
        int avg = sum[length-1]/length;
        int minMv = INT_MIN;
        for(int i=1;i<length;i++){
            int left = sum[i-1] - avg*i;
            int right = sum[length-1] - sum[i] - avg*(length-1-i);
            if(left<0 && right<0)
                minMv = max(minMv, -left-right);
            else if(left>0 && right>0)
                minMv = max(minMv, max(left, right));
            else
                minMv = max(minMv, max(abs(left), abs(right)));
        }
        return minMv;
    }
};
```

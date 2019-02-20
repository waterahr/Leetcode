# 764.最大加号标志

对于第i行第j列的元素grid[i][j]表示的是这个元素的plus sign的等级，初始化不在mines中的元素对应的grid值为较大值（只要大于N/2即可），在mines中的元素对应的grid值为0。不在mines中的元素，其grid[i][j]=左右上下四个方向最少的连续1的个数（不包括自己）+1。

```cpp
class Solution {
public:
    int orderOfLargestPlusSign(int N, vector<vector<int>>& mines) {
        vector<vector<int>> grid(N, vector<int>(N, N));
        for(auto& m : mines){
            grid[m[0]][m[1]] = 0;
        }
        for(int i = 0; i < N; i++){
            int l = 0, r = 0, u = 0, d = 0;
            for(int j = 0, k = N - 1; j < N; j++, k--){
                grid[i][j] = min(grid[i][j], l = (grid[i][j] == 0 ? 0 : l + 1));
                grid[i][k] = min(grid[i][k], r = (grid[i][k] == 0 ? 0 : r + 1));
                grid[j][i] = min(grid[j][i], u = (grid[j][i] == 0 ? 0 : u + 1));
                grid[k][i] = min(grid[k][i], d = (grid[k][i] == 0 ? 0 : d + 1));
            }
        }
        int order = 0;
        for(int i = 0; i < N; i++)
            for(int j = 0; j < N; j++)
                order = max(order, grid[i][j]);
        return order;
    }
};
```

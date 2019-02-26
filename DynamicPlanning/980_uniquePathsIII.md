# 980.不同路径III

```cpp
class Solution {
public:
    int uniquePathsIII(vector<vector<int>>& grid) {
        int x = 0, y = 0, steps = 1;
        for(int i=0; i<grid.size(); i++)
            for(int j=0; j<grid[0].size(); j++){
                if(grid[i][j] == 0)
                    steps++;
                else if(grid[i][j] == 1){
                    x = i;
                    y = j;
                }
            }
        return dfs(grid, x, y, steps);
    }
    
private:
    int dfs(vector<vector<int>>& grid, int x, int y, int steps){
        if(grid[x][y] == 2 && steps == 0)
            return 1;
        else if(grid[x][y] == 2)
            return 0;
        int count = 0;
        grid[x][y] = -1;
        if(x-1 >= 0 && grid[x-1][y] != -1)
            count += dfs(grid, x-1, y, steps-1);
        if(x+1 < grid.size() && grid[x+1][y] != -1)
            count += dfs(grid, x+1, y, steps-1);
        if(y-1 >= 0 && grid[x][y-1] != -1)
            count += dfs(grid, x, y-1, steps-1);
        if(y+1 < grid[0].size() && grid[x][y+1] != -1)
            count += dfs(grid, x, y+1, steps-1);
        grid[x][y] = 0;
        return count;
    }
};
```

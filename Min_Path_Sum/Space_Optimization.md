# Minimum path Sum Problem in 2D with Space Optimization Approach

## Approach

If there is prev row & prev col, we can optimize it.
Since, it is only **dp[i-1][j] & dp[i][j-1]**, hence, we can see that, we only require the previous element and the previous row.
So, we will declare two arrays, one denoting the previous array while other will be denoting current array and we will update the prev to curr on each next row.

## Code

```c++
    int minPathSum(vector<vector<int>>& grid) {
        int m=grid.size();
        int n= grid[0].size();

        vector<int> prev(n,0);
        for(int i=0;i<m;i++){
            vector<int> curr(n,0);
            for(int j=0;j<n;j++){
                if(i==0 && j==0) curr[j]=grid[0][0];
                else{
                    int up=INT_MAX, left=INT_MAX;
                    if(i>0) up = grid[i][j] + prev[j];
                    if(j>0) left = grid[i][j] + curr[j-1];
                    curr[j]=min(up,left);
                }
            }
            prev=curr;
        }
        return prev[n-1];
    }
```

**TC:** O(m\*n)

**SC:** O(n)

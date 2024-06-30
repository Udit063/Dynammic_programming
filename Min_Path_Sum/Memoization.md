# Minimum path Sum Problem in 2D with Memoization Approach

## Approach

Since, we have to find all the possible ways to go from **(0,0)** to **(m-1, n-1)**. So, we will use recursion here. Also, there are only two ways, to go **right** or to go **down**. If we start from the end, then it's just the opposite, up and left.

We have two variables **(rows and cols)** to express it instead of indexes.
Now for performing the stuff, we have two paths, to go up or to go left. Then, find the min of the up and left to find the min path sum and add it to the current cell.

For memoization, declare a dp 2D array and initialize with -1. Just call it before going up or left and at last store the sum in the 2D array.

## Code

```c++
    int f(int i,int j, vector<vector<int>>& grid, vector<vector<int>>&dp){
        if(i==0 && j==0) return grid[i][j];
        if(i<0 || j<0) return INT_MAX;
        if(dp[i][j]!=-1) return dp[i][j];
        int up = f(i-1, j, grid, dp);
        int left = f(i, j-1, grid, dp);
        return dp[i][j] = grid[i][j] + min(up,left);
    }

    int minPathSum(vector<vector<int>>& grid) {
        int m=grid.size();
        int n= grid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,-1));
        return f(m-1, n-1, grid, dp);
    }
```

**TC:** O(m\*n)

**SC:** O((m-1) + (n-1)) + O(m\*n)

<!-- first for path sum and second for dp declaration -->

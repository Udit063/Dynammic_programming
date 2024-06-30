# Unique path find Problem 2 with obstacles in 2D with Memoization Approach

## Approach

We know how to find the the unique paths as done earlier. Now, there is an obstacle which when reaches, then there is no option to move, means the path is wrong. So, just add the 1 more base condition **if(arr[i][j]==1) return 0;**.

## Code

```c++
     int f(int i, int j, vector<vector<int>>& dp, vector<vector<int>>& obstacleGrid){
        if(i >= 0 && j >= 0 && obstacleGrid[i][j] == 1) return 0;
        if(i==0 && j==0) return 1;
        if(i<0 || j<0) return 0;
        if(dp[i][j] != -1) return dp[i][j];
        int up=f(i-1,j,dp,obstacleGrid);
        int left = f(i,j-1,dp,obstacleGrid);
        return dp[i][j]=up+left;
    }

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m=obstacleGrid.size();
        int n=obstacleGrid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,-1));
        return f(m-1, n-1, dp, obstacleGrid);
    }
```

**TC:** O(m\*n)

<!-- first for path sum and second for dp declaration -->

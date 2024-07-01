# Minimum path Sum Problem in Triangle with Memoization Approach

## Approach

Now, for finding min path sum in triangle, we can go only **downwards** or **diagonally right**. We have to move from **(0,0)** to **(n-1,j)**, i.e., last row.
Since, we have variable elements in the last row from where it can be ended, so, we have to start from **(0,0)** as it will be single fixed point.

Now, perform the operation like down and diagonal and return the min of both.

For **memoization**, declare a dp 2D array and initialize with -1. Just check it before going down or diag and at last store the sum in the 2D array.

## Code

```c++
    <int>>& triangle, vector<vector<int>>& dp, int n){
        if(i==n-1) return triangle[i][j];
        if(dp[i][j] != -1) return dp[i][j];
        int down = triangle[i][j] + f(i+1, j, triangle, dp, n);
        int diag = triangle[i][j] + f(i+1, j+1, triangle, dp, n);
        return dp[i][j]=min(down, diag);
    }

    int minimumTotal(vector<vector<int>>& triangle) {
        int n=triangle.size();
        vector<vector<int>>dp(n,vector<int>(n,-1));
        return f(0, 0, triangle, dp, n);
    }
```

**TC:** 2\*\*(1+2+3+.....+n)

**SC:** O(n)

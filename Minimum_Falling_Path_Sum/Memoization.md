# Minimum Falling Path Sum Problem with Memoization Approach

## Approach

Since, we have different starting points and different ending points. So, we will have to check for all the starting point or the ending point and then accordingly go upwards diagonally left or diagonally right.

For Base cases

1. First will be at **destination**, when we reaches the end.
2. Second base case will be when we get **out of boundaries**, when **(j<0)** or **(j>=m)**.

## Code

```c++
    int f(int i, int j, vector<vector<int>>& matrix, int m, vector<vector<int>>& dp){
        if(j<0 || j>=m) return INT_MAX;
        if(i == 0) return matrix[i][j];
        if(dp[i][j] != -1) return dp[i][j];
        int up = matrix[i][j] + f(i-1, j, matrix, m, dp);

        int diagRight = matrix[i][j] + f(i-1, j+1, matrix, m, dp);
        if(j+1 < m) diagRight = matrix[i][j] + f(i-1, j+1, matrix, m, dp);

        int diagLeft = matrix[i][j] + f(i-1, j-1, matrix, m, dp);
        if(j-1 >= 0) diagLeft = matrix[i][j] + f(i-1, j-1, matrix, m, dp);

        return dp[i][j] = min(up, min(diagRight,diagLeft));
    }

    int minFallingPathSum(vector<vector<int>>& matrix) {
        int m = matrix[0].size();
        int n=matrix.size();
        int mini = INT_MAX;
        vector<vector<int>> dp(n,vector<int>(m,-1));
        for(int j=0;j<m;j++){
            mini =  min(mini, f(n-1,j, matrix, m, dp));
        }
        return mini;
    }
```

**TC:** O(3^n)

**SC:** O(n)

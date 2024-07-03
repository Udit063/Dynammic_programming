# Minimum Falling Path Sum Problem with Tabulation Approach

## Approach

Sometimes, memoization does give **Time Exceeded problem** due to excessive recursion, so we use tabulation for optimization.

For Tabulation, first check and declare the base cases after assigning same dp array.

Base Cases:-

1. When (i==0) -> j=0,1,2,....,(m-1)
2. for (j=0 -> m-1) -> dp[0][j] = a[0][j];

For rest the code will be same and **min element** will me **min( dp[n-1][0] , dp[n-1][m-1] )**

## Code

```c++
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int m = matrix[0].size();
        int n=matrix.size();
        vector<vector<int>> dp(n,vector<int>(m,-1));

        for(int j=0;j<m;j++){
            dp[0][j] = matrix[0][j];
        }

        for(int i=1 ;i<n;i++){
            for(int j=0;j<m;j++){
                int up = matrix[i][j] + dp[i-1][j];
                int leftDiag = INT_MAX;
                if(j-1 >= 0) leftDiag = matrix[i][j] + dp[i-1][j-1];
                int rightDiag = INT_MAX;
                if(j+1 < m) rightDiag = matrix[i][j] + dp[i-1][j+1];

                dp[i][j] = min(up, min(leftDiag, rightDiag));
            }
        }
        int mini = dp[n-1][0];
        for(int j=1;j<m;j++){
            mini = min(mini, dp[n-1][j]);
        }
        return mini;
    }
```

**TC:** O(n\*m) + O(n)

**SC:** O(n\*m)

# Unique path find Problem in 2D with Tabulation Approach

## Approach

For tabulation, initialize the base case, then convert it into for loops. After converting it, just copy paste the entire code.

## Code

```c++
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n,-1));
        dp[0][0]=1;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(i==0 && j==0) continue;
                int up=0, left=0;
                if(i>0) up=dp[i-1][j];
                if(j>0) left=dp[i][j-1];
                dp[i][j]=up+left;
            }
        }
        return dp[m-1][n-1];
    }
```

**TC:** O(m\*n)

**SC:** O(m\*n)

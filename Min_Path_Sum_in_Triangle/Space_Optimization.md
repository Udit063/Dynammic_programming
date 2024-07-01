# Minimum path Sum Problem in Triangle with Space Optimization Approach

## Approach

Since, we go from **(0 -> n-1)** in **recursion** and we know that _tabulation is just the opposite of recursion_. So, in **tabulation**, we will go from **(n-1 -> 0)**.

In tabulation, the base case may vary and will be equal to n. So, we will first declare all the base cases in the last row and apply the for loops from the 2nd last row, rest logic will be same.

## Code

```c++
    int minimumTotal(vector<vector<int>>& triangle) {
        int n=triangle.size();
        vector<vector<int>>dp(n,vector<int>(n,-1));

        for(int j=0;j<n;j++) dp[n-1][j] = triangle[n-1][j]; //Base case

        for(int i=n-2;i>=0;i--){
            for(int j=i;j>=0;j--){
                int down = triangle[i][j] + dp[i+1][j];
                int diag = triangle[i][j] + dp[i+1][j+1];
                dp[i][j] = min(down, diag);
            }
        }
        return dp[0][0];
    }
```

**TC:** O(n\*n)

**SC:** O(n\*n)

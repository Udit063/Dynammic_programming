# Count no of Square Submatrices using Tabulation approach

## Approach

In this question, we are given a matrix with **0's** and **1's**, and we have to find out **total no of square submatrices**. For ex,

1 0 1

1 1 1

1 1 0

hence, total no of **square matrices** formed will be **7**.

Now, to solve this we will **take each cell** and see how many square matrices can be formed with keeping that **cell at right bottom of square**. For ex, for above matrix, **no of squares at each cell** can be formed as:-

1 0 1 -> 1 0 1

1 1 1 -> 1 1 1

1 1 0 -> 1 2 0

hence, our **answer** will be the **total sum of all this new matrix**. In order to achieve this, we take a **dp[n][m] array** and we will take our **first row** and **first column** as it is and when **matrix[i][j] = 0**, then our **dp[i][j] = 0**. But, **if(dp[i][j] != 0)**, then we will take the **min** of the **above cell**, **diagonal cell** and **left cell** to check square matrix and **add 1** to it in order to find no the **square matrix**.

## Code

```c++
    int countSquares(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        vector<vector<int>> dp(n, vector<int>(m, 0));
        int ans=0;

        for(int j=0; j<m; j++) dp[0][j] = matrix[0][j];
        for(int i=0; i<n; i++) dp[i][0] = matrix[i][0];

        for(int i=1; i<n; i++){
            for(int j=1; j<m; j++){
                if(matrix[i][j] == 0) dp[i][j] = 0;
                else{
                    dp[i][j] = min(dp[i-1][j], min(dp[i-1][j-1], dp[i][j-1])) + 1;
                }
            }
        }
        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                ans += dp[i][j];
            }
        }
        return ans;
    }
```

**TC:** O(n\*m)

**SC:** O(n\*m)

# Minimum Falling Path Sum Problem with Space Optimization Approach

## Approach

Since, as we can see that we require **dp[i-1]**, means the previous row and **dp[j]**, means the current row. So, we can space optimize it using 2 arrays _prev_ and _curr_, taking the values from prev array and storing the result in curr array and later change the **prev = curr**.

## Code

```c++
    int minFallingPathSum(vector<vector<int>> &matrix)
    {
        int m = matrix[0].size();
        int n = matrix.size();

        vector<int> prev(n, 0);
        for (int j = 0; j < m; j++)
        {
            prev[j] = matrix[0][j];
        }
        for (int i = 1; i < n; i++)
        {
            vector<int> curr(n, 0);
            for (int j = 0; j < m; j++)
            {
                int up = matrix[i][j] + prev[j];
                int leftDiag = INT_MAX;
                if (j - 1 >= 0)
                    leftDiag = matrix[i][j] + prev[j - 1];
                int rightDiag = INT_MAX;
                if (j + 1 < m)
                    rightDiag = matrix[i][j] + prev[j + 1];

                curr[j] = min(up, min(leftDiag, rightDiag));
            }
            prev = curr;
        }
        int mini = prev[0];
        for (int j = 1; j < m; j++)
        {
            mini = min(mini, prev[j]);
        }
        return mini;
    }

```

**TC:** O(n\*m) + O(n)

**SC:** O(n)

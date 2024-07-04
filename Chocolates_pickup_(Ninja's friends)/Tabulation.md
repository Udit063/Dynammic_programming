# Chocolates Pickup (Ninja's friends) Problem with Tabulation Approach

## Approach

(Top -> down => opposite of recursion)

For tabulation, there will be multiple base cases, like for an ending point of alice **(0 -> m-1)** there will be **(0-> m-1)** cases for bob.

## Code

```c++
    int solve(int n, int m, vector<vector<int>>& grid) {
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(m, vector<int>(m,0)));

        for (int j1 = 0; j1 < m; j1++) {
            for (int j2 = 0; j2 < m; j2++) {
                if (j1 == j2)
                    dp[n - 1][j1][j2] = grid[n - 1][j1];
                else
                    dp[n - 1][j1][j2] = grid[n - 1][j1] + grid[n - 1][j2];
            }
        }

        for (int i = n - 2; i >= 0; i--) {
            for (int j1 = 0; j1 < m; j1++) {
                for (int j2 = 0; j2 < m; j2++) {
                    int maxi = -1e8;
                    for (int k = -1; k <= 1; k++) {
                        for (int l = -1; l <= 1; l++) {
                            int value = 0;
                            if (j1 == j2)
                                value = grid[i][j1];
                            else
                                value = grid[i][j1] + grid[i][j2];

                            if (j1 + k >= 0 && j1 + k < m && j2 + l >= 0 && j2 + l < m) {
                                value += dp[i + 1][j1 + k][j2 + l];
                            } else {
                                value += -1e8;
                            }

                            maxi = max(maxi, value);
                        }
                    }
                dp[i][j1][j2] = maxi;
                }
            }
        }
        return dp[0][0][m - 1];
    }
```

**TC:** O(n\*m\*m)

**SC:** O(n\*m\*m)

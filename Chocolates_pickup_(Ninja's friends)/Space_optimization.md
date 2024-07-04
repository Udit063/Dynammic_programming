# Chocolates Pickup (Ninja's friends) Problem with Space Optimization Approach

## Approach

For **2D array**, we require **1D array** for space optimization. Hence, for **3D array**, we will require **2D array** for space optimization.

Also, we can see that, we are required with the **current row (d[i][][])** and the **front ro (d[i+1][][])w** for computation, hence, we will be required with **2 - 2D arrays**.

## Code

```c++
    int solve(int n, int m, vector<vector<int>>& grid) {
        vector<vector<int>> front(m, vector<int>(m,0));
        vector<vector<int>> curr(m, vector<int>(m,0));

        for (int j1 = 0; j1 < m; j1++) {
            for (int j2 = 0; j2 < m; j2++) {
                if (j1 == j2)
                    front[j1][j2] = grid[n - 1][j1];
                else
                    front[j1][j2] = grid[n - 1][j1] + grid[n - 1][j2];
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
                                value += front[j1 + k][j2 + l];
                            } else {
                                value += -1e8;
                            }

                            maxi = max(maxi, value);
                        }
                    }
                    curr[j1][j2] = maxi;
                }
            }
            front = curr;
        }
        return front[0][m - 1];
    }
```

**TC:** O((n\*m*m) * 9)

**SC:** O(m\*m)

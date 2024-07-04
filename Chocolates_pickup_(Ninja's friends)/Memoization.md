# Chocolates Pickup (Ninja's friends) Problem with Memoization Approach

## Approach

As we can see that the starting position is fixed, **first** and **last**, for both the friends. So, we can see that we have **fixed starting points** but **variable ending points**, so, we will go from up to down.

Since, every cell will be counted once, even if both friends visited the same cell, so, both friends have to come downwards at the same time so that we can check if they collide on the same cell or not, hence, **i(row)** will remain same for both.

So, to express in terms of (i,j) -> we have **(i, j1)** and **(i, j2)** for both friends respectively.

Base cases:-

1. Out of bound -> when **(j<0)** or **(j>=m)**
2. Destination -> when **(i==m-1)**

Since, we have 3 paths for both friends, **downLeft, down and downRight**. So, for every movement of Alice, Bob has 3 paths to move.
It means that we have total 9 combo paths to check. Either manually add all 9 paths or do call for _for_ loop like for every 1 path, bob takes all 3 paths.

## Code

```c++
    int f(int i, int j1, int j2, vector<vector<int>>& grid, int n, int m, vector<int> a, vector<vector<vector<int>>>& dp){
        if(j1<0 || j1 >=m || j2<0 || j2>=m) return -1e8;
        if(i==(n-1)){
            if(j1==j2) return grid[i][j1]; // when destination is same
            else return grid[i][j1] + grid[i][j2];
        }
        if(dp[i][j1][j2] != -1) return dp[i][j1][j2];
        int maxi=INT_MIN;
        for(int k=0; k<3;k++){
            for(int l=0;l<3;l++){
                if(j1==j2) maxi = max(maxi, grid[i][j1] + f(i+1, j1+a[k], j2+a[l], grid, n, m, a, dp));
                else maxi = max(maxi, grid[i][j1] + grid[i][j2] + f(i+1, j1+a[k], j2+a[l], grid, n, m, a, dp));
            }
        }
        return dp[i][j1][j2] = maxi;

    }

    int solve(int n, int m, vector<vector<int>>& grid) {
        vector<int> a={-1,0,1}; // for exploring paths (downLeft, down, downRight)
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(m, vector<int>(m,-1)));
        return f(0, 0, m-1, grid, n, m , a, dp);
    }
```

**TC:** O((n\*m*m) * 9)

**SC:** O(n) + O(n\*m\*m)

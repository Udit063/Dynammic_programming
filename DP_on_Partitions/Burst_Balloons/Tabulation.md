# Burst Balloons Problem using Tabulation Approach

## Approach

We need to optimize **recursion stack space** in memoization, hence, we will use **tabulation**.

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in **recursion**, we had went from **(1 -> n for i and n -> 1 for j)**, hence, in **tabulation**, we will go from **(n -> 1 for i and 1 -> n for j)**. **DP array** will be of size **dp[n+2][n+2]** as bcz whenever we do **(ind+1)** in tabulation, it **doesn't go out of bound**.

For Tabulation:-

1. Declare base case
2. Make the **for** loop for changing variable **(i & j)**
3. Copy recursion & modify it.

## Code

```c++
    int maxCoins(vector<int>& nums) {
        int n = nums.size();
        nums.push_back(1);
        nums.insert(nums.begin(), 1);

        vector<vector<int>> dp(n+2, vector<int>(n+2, 0));
        for(int i=n; i>=1; i--){
            for(int j=1; j<=n; j++){
                if(i>j) continue;
                int maxi = INT_MIN;
                for(int ind=i; ind<=j; ind++){
                    int cost = nums[i-1]*nums[ind]*nums[j+1] + dp[i][ind-1] + dp[ind+1][j];
                    maxi = max(maxi, cost);
                }
                dp[i][j] = maxi;
            }
        }
        return dp[1][n];
    }
```

**TC:** O(n*n*n)

**SC:** O(n\*n)

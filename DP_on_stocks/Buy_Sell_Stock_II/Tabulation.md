# Buy and Sell Stock II using Tabulation Approach

## Approach

We need to optimize **recursion stack space** in memoization, hence, we will use **tabulation**.

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in **recursion**, we had went from **(0 -> n)**, hence, in **tabulation**, we will go from **(n -> 0)**.

For Tabulation:-

1. Declare base case
2. Make the **for** loop for changing variable **((n-1 -> 0) for ind & (0 -> 1) for buy)**
3. Copy recursion & modify it.

For Base case, when **(ind == n)**, return 0; **Base case => dp[n][buy] = 0**

## Code

```c++
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        vector<vector<int>> dp(n+1, vector<int>(2, 0));
        dp[n][0] = dp[n][1] = 0;

        for(int ind = n-1; ind>=0; ind--){
            for(int buy=0; buy<2; buy++){
                int profit = 0;
                if(buy) profit = max(-prices[ind] + dp[ind+1][0], 0 + dp[ind+1][1]);
                else profit = max(prices[ind] + dp[ind+1][1], 0 + dp[ind+1][0]);
                dp[ind][buy] = profit;
            }
        }
        return dp[0][1];
    }
```

**TC:** O(n\*2)

**SC:** O(n\*2)

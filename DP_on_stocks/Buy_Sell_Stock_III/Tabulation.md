# Buy and Sell Stock III using Tabulation Approach

## Approach

We need to optimize **recursion stack space** in memoization, hence, we will use **tabulation**.

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in **recursion**, we had went from **(0 -> n)**, hence, in **tabulation**, we will go from **(n -> 0)**.

For Tabulation:-

1. Declare base case
2. Make the **for** loop for changing variable **(n-1 -> 0) for ind & (0 -> 1) for buy & (0 -> 2) for cap**
3. Copy recursion & modify it.

For Base case, when **(ind == n)**, return 0; **Base case => dp[n][buy][cap] = 0**. WHen **(cap == 0)**, return 0; **Base case => dp[n][buy][cap] = 0**.

## Code

```c++
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        vector<vector<vector<int>>> dp(n+1, vector<vector<int>>(2, vector<int>(3, 0)));

        // base case is not needed as it is already 0
        for(int ind=n-1; ind>=0; ind--){
            for(int buy=0; buy<=1; buy++){
                for(int cap=1; cap<=2; cap++){
                    int profit = 0;
                    if(buy) profit = max(-prices[ind] + dp[ind+1][0][cap], 0 + dp[ind+1][1][cap]);
                    else profit = max(prices[ind] + dp[ind+1][1][cap-1], 0 + dp[ind+1][0][cap]);

                    dp[ind][buy][cap] = profit;
                }
            }
        }
        return dp[0][1][2];
    }
```

**TC:** O(n\*2\*3)

**SC:** O(n\*2\*3)

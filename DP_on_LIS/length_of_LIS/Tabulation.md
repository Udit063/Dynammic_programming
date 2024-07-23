# Length of LIS using Tabulation Approach

## Approach

We need to optimize **recursion stack space** in memoization, hence, we will use **tabulation**.

For **tabulation(down -> top)**, first delcare the same dp array and base case. Since, in **recursion**, we had went from **(0 -> n)**, hence, in **tabulation**, we will go from **(n -> 0)**.

For Tabulation:-

1. Declare base case
2. Make the **for** loop for changing variable **((n-1 -> 0) for ind & (ind-1 -> -1) for prev_ind)**. Since, **prev_ind** is **just before** element, hence we will initialize it with **(ind-1)**
3. Copy recursion & modify it. Also, don't forget to do **coordinate shifting**.

For Base case, when **(ind == n)**, return 0; **Base case => dp[n][prev] = 0**

## Code

```c++
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();

        vector<vector<int>> dp(n+1, vector<int>(n+1,0));

        for(int ind=n-1; ind>=0; ind--){
            for(int prev_ind = ind-1; prev_ind >= -1; prev_ind--){
                int not_take = 0 + dp[ind+1][prev_ind+1];
                int take = INT_MIN;
                if(prev_ind == -1 || nums[ind] > nums[prev_ind]) take = 1 + dp[ind+1][ind+1];

                dp[ind][prev_ind+1] = max(take, not_take);
            }
        }
        return dp[0][-1+1];
    }
```

**TC:** O(n\*n)

**SC:** O(n\*n)

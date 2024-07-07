# Partition min difference Problem with Tabulation Approach

## Approach

The way we had done in the **subset sum problem**, **Tabulation Method**, we will observe that the **last element** of **last row** give us the answer either if it is **T/F** when divided into two subsets with **sum S1** **and sum S2** resp.

If we see in subset problem, then this will be the **tabulation matrix** for **n=5** and **target=7**. So, our answer will me **dp[4][7] = True/False**. Similarly we can check for all the cells of last row, either the subset **S1** sum contains the target **sum (0,1,....,7)** or not.

|     | #0  | #1  | #2  | #3  | #4  | #5  | #6  | #7  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | --- |
| #0  |  T  |  T  |     |     |     |     |     |     |
| #1  |  T  |  X  |  X  |  X  |  X  |  X  |  X  | X   |
| #2  |  T  |  X  |  X  |  X  |  X  |  X  |  X  | X   |
| #3  |  T  |  X  |  X  |  X  |  X  |  X  |  X  | X   |
| #4  |  T  |  X  |  X  |  X  |  X  |  X  |  X  | X   |

Now, when we found that the **S1** sums which are possible, then we can get the sum **S2** by **subtracting** it from the **total sum**.

Hence, return the **minimum** of **abs(S1-S2)**. But, this will only work for **positive integers**.

## Code

```c++
    int minimumDifference(vector<int>& nums) {
        int n=nums.size();

        int total_sum = 0;
        for(int i = 0; i < n; i++) total_sum += nums[i];

        int sum = total_sum;

        vector<vector<bool>> dp(n,vector<bool>(sum+1, 0));

        for(int i=0; i<n; i++) dp[i][0] = true;

        if(nums[0] <= sum) dp[0][nums[0]] = true;

        for(int i=1; i<n; i++){
            for(int target=1; target <= sum; target++){
                bool not_take = dp[i-1][target];
                bool take = false;
                if(target >= nums[i]) take = dp[i-1][target-nums[i]];
                dp[i][target] = not_take | take;
            }
        }

        // dp[n-1][col -> 0....total_sum] will give the S1
        int mini = 1e9;
        for(int s1=0; s1<=total_sum/2; s1++){
            if(dp[n-1][s1] == true) mini = min(mini, abs((total_sum - s1) - s1));
        }
        return mini;
    }
```

**TC:** O(n\*sum)

**SC:** O(n\*sum)

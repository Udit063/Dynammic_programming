# Length of LIS using Tabulation Best Approach

## Approach

Just take a **dp[n] array** and **initialize** it with **1**, as bcz every element will have **atleast 1 LIS**. Let's take an example, **a[] = [5, 4, 11, 1, 16, 8]** and **dp[i]** will be storing the **length of LIS till ith index**, i.e., **dp[n] = [1, 1, 2, 1, 3, 2]** and **ans** will be **max(dp[i])**. To achieve this array, we first need to check which **previous elements are shorter** then **add 1** to their **corresponding dp array** and **compare with the dp[i]** and only **update** if it is **greater**. Just do a dry run for better understanding.

This approach is important to **trace back the LIS**.

## Code

```c++
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n, 1);
        int maxi = 1;

        for(int ind=0; ind<n; ind++){
            for(int prev_ind = 0; prev_ind < ind; prev_ind++){
                if(nums[ind] > nums[prev_ind]) dp[ind] = max(1+dp[prev_ind], dp[ind]);
            }
            maxi = max(maxi, dp[ind]);
        }
        return maxi;
    }
```

**TC:** O(n\*n)

**SC:** O(n)

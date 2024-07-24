# Number of LIS using Tabulation Best Approach

## Approach

For getting **total number of LIS**, we will use the **Tabulation Best Approach**, in which we were storing the **maximum length of the LIS** till that index. Now, in this question, we will take 1 more array **cnt[n]** and initialize it with **1**. We will check, whenever **dp[i] gets updated**, then **cnt[i] will also get updated** **only** **after checking** it. If, the **length(value) increases in dp[i]**, then **cnt[i]** should remain same as from the prev, **cnt[prev_ind]** from which **dp[i]** have been updated and **if(dp[i]+1 == dp[i])** then **cnt[i] += cnt[prev_ind]**.

At last, return the **max(cnt[i])**.

## Code

```c++
    int findNumberOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n, 1), cnt(n, 1);
        int maxi = 1;

        for(int ind=0; ind<n; ind++){
            for(int prev_ind = 0; prev_ind < ind; prev_ind++){
                if(nums[ind] > nums[prev_ind] && 1+dp[prev_ind] >  dp[ind]) {
                    dp[ind] = 1 + dp[prev_ind];
                    // inherit
                    cnt[ind] = cnt[prev_ind];
                }
                else if(nums[ind] > nums[prev_ind] && dp[prev_ind]+1 == dp[ind]){ // case when got more than 1 subsequence
                    // increase the count
                    cnt[ind] += cnt[prev_ind];
                }
            }
            maxi = max(maxi, dp[ind]);
        }

        int count = 0;
        for(int i = 0; i<n; i++){
            if(dp[i] == maxi) count += cnt[i];
        }
        return count;
    }
```

**TC:** O(n\*n)

**SC:** O(n)

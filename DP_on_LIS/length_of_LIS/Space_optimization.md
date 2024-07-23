# Length of LIS using Space Optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **next** and **curr** and change accourdingly.

## Code

```c++
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();

        vector<int> next(n+1, 0), curr(n+1, 0);

        for(int ind=n-1; ind>=0; ind--){
            for(int prev_ind = ind-1; prev_ind >= -1; prev_ind--){
                int not_take = 0 + next[prev_ind+1];
                int take = INT_MIN;
                if(prev_ind == -1 || nums[ind] > nums[prev_ind]) take = 1 + next[ind+1];

                curr[prev_ind+1] = max(take, not_take);
            }
            next = curr;
        }
        return next[-1+1];
    }
```

**TC:** O(n\*n)

**SC:** O(n)

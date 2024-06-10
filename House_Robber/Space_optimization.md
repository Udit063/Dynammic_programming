# House Robber Problem with Space Optimization Approach

## Approach

If we see the prev codes then we can see there will be needed only two variables denoting **dp[n-1]** and **dp[n-2]** as well as a current variable and update these variables as we move forward.

Also, if we see, we were returning **dp[n-1]** (when 'i==n'). So, in this case, we will be returning the **prev** variable.

## Code

```c++
    int rob(vector<int>& nums) {
        int n=nums.size();
        dp[0]=nums[0];
        int prev = nums[0];
        int prev2=0;
        for(int i=1;i<n;i++){
            int pick = nums[i];
            if(i>1) pick += prev2;
            int non_pick = 0 + prev;
            int curr = max( pick, non_pick);
            prev2=prev;
            prev=curr;
        }
        return prev;
    }
```

**TC:** O(n)

**SC:** O(1)

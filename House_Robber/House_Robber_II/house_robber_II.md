# House Robber II Problem

This is the problem when houses are in a circle.

## Approach

Since, houses are in a circle, then the first and last house will be adjacent so we will have to consider any one of it.

So, at first, we will remove the first element and apply the same logic in the rest houses as done previously and similarly do with the last house.

The ans with the maximum sum will be our answer.

## Code

```c++
    int maxAdjSum(vector<int>& nums) {
        int n=nums.size();

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

    int rob(vector<int>& nums) {
        int n=nums.size();
        if(n==1) return nums[0];
        vector<int> temp1, temp2;
        for(int i=0;i<n;i++){
            if(i != 0) temp1.push_back(nums[i]);
            if(i != n-1) temp2.push_back(nums[i]);
        }
        return max(maxAdjSum(temp1), maxAdjSum(temp2));
    }
```

**TC:** O(n)

**SC:** O(1)

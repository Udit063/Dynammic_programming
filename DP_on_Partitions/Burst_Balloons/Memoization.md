# Burst Balloons Problem using Memoization Approach

## Approach

In this question, we will be given an array, for ex, **[3, 1, 5, 8]**, and we have yo burst the balloons such that total no of coins is **maximum**. **No. of coins for ith element = A[i-1] X A[i] X A[i+1]**. For ex, if we burst **[3, 1, 5, 8]**, such that at first we **burst 1**, **no of coins = 3 x 1 x 5**, then we left with **[3, 5, 8]**, now if we **burst 5**, **no of coins = 3 x 5 x 8**, then we left with **[3, 8]**, now on **bursting 3**, **no of coins = 1 x 3 x 8**, and at last array left = **[8]** and **no of coins = 1 x 8 x 1**, hence **total no of coins = 167**, which is the **maximum**.

Before starting, **add 1** at the **beginning** as well as at the **end** of the array.

Since, anyone can be **first from starting to ending index**, hence, we will use **partition DP**. But when we burst any element, for ex when we had **burst 1**, then we **cannot** do partitions like **[3] and [5,8]** independently as because **3 will require 5** as well as **5 will require 3**. Hence, they are **dependent** on each other.

Hence, we will **start from ending to starting**. For ex, we will **burst 8 first** which will be at **end** and hence, **no of coins = 1 x 8 x 1**, for **second last**, **8 must be present** there in order to **burst it at last**. Now, for ex we **burst 3** at **second last**, then **no of coins = 1 x 3 x 8** from many like **[3, 8] or [1, 8] or [5, 8]** and similarly for the rest. These can be said as **independent**, as because now on **bursting 5** now, **3 and 8 will already present there** from the second last and 5 doesn't require the need for 1 element.

For **base case**, when **(i>j)**, **return 0** as no other operation can be done now. We have to solve it even when **(i==j)**.

Now **value for coins = A[i-1] _ A[ind] _ A[j+1]** where **ind** will be bursting elements from **(i -> j)**. For further operations, it will be, **f(i, ind-1) + f(ind+1, j)** for the **partitions**.

Now, after this step, return **max of all costs**.

## Code

```c++
    int f(int i, int j, vector<int>& nums, vector<vector<int>>& dp){
        if(i > j) return 0;
        int maxi = INT_MIN;
        if(dp[i][j] != -1) return dp[i][j];

        for(int ind=i; ind<=j; ind++){
            int cost = nums[i-1]*nums[ind]*nums[j+1] + f(i, ind-1, nums, dp) + f(ind+1, j, nums, dp);
            maxi = max(maxi, cost);
        }
        return dp[i][j] = maxi;
    }

    int maxCoins(vector<int>& nums) {
        int n = nums.size();
        nums.push_back(1);
        nums.insert(nums.begin(), 1);
        vector<vector<int>> dp(n+1, vector<int>(n+1, -1));
        return f(1, n, nums, dp);
    }
```

**TC:** O(n\*n\*n)

**SC:** O(n\*n) + O(n)

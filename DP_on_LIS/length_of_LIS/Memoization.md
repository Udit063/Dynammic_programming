# Length of Longest Increasing Subsequence using Memoization Approach

## Approach

In this question, we are given an array and we have to find the **length of Longest Increasing Subsequence** of an array.

Since, we have to find all the subsequences and find out the maximum length of increasing LIS, hence we have to **try all ways**, hence use **recursion**.

For recursion:-

1. Express in terms of **(index, prev_ind)**. We have to take the **previous value** also to check and take values only in the **increasing order**.
2. Explore all possible ways on that day like **(take or not_take)**. When we **take**, **add 1** to the **length**, and if we **not_take**, don't add anything.
3. return the **max length** of the both.

For **base case**, whenever the array ends, means we have nothing left and we came out of the array, hence **return 0**.

Since, it will create an **overlapping subproblem**, hence, we will use **memoization**.

We can see that storing **-1** for **prev** in dp **will not be possible**, hence, we will do **coordinate shifting**, like **storing value of index 0 at index 1, and so on**. And also check, if prev == -1, means we are taking first value, so add this case also in taking the element.

For memoization, just take a **dp[n][n+1]** array and store the result in this array. Also, check if any value exists in this array before moving forward.

## Code

```c++
    int f(int ind, int prev_ind, int n, vector<int>& nums, vector<vector<int>>& dp){
        if(ind == n) return 0;
        if(dp[ind][prev_ind+1] != -1) return dp[ind][prev_ind+1];

        int not_take = 0 + f(ind+1, prev_ind, n, nums, dp);
        int take = INT_MIN;
        if(prev_ind == -1 || nums[ind] > nums[prev_ind]) take = 1 + f(ind+1, ind, n, nums, dp);

        return dp[ind][prev_ind+1] = max(take, not_take);
    }

    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<vector<int>> dp(n, vector<int>(n+1,-1));
        return f(0, -1 , n, nums, dp);
    }
```

**TC:** O(n\*n)

**SC:** O(n\*n) + O(n)

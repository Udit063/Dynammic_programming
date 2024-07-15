# Longest common Subsequence Problem using Memoization Approach

## Approach

In this question, we are given **2 strings** and we need to find the **maximum common substring** in both. So, we will need to find all the subsequences of both the string, hence, we will use **recursion** for it.

For recursion, we will take **2 indexes**, **ind1 for string1** and **ind2 for string2** which will be pointing at the last character of the string. If both **characters matches (Base Case)**, then the **indexes** of both get **reduced to 1** and also **add 1** before reducing. But, if the string **characters match**, then keep **ind1 same** and **reduce ind2** for checking and similarly take **ind2 same** and **reduce ind1** for checking and return the max subsequence from both.

## Code

```c++
    int f(int ind1, int ind2, string text1, string text2, vector<vector<int>>& dp){
        if(ind1 < 0 || ind2 < 0) return 0;
        if(dp[ind1][ind2] != -1) return dp[ind1][ind2];
        if(text1[ind1] == text2[ind2]) return 1 + f(ind1-1, ind2-1, text1, text2, dp);
        return dp[ind1][ind2] = max(f(ind1-1, ind2, text1, text2, dp), f(ind1, ind2-1, text1, text2, dp));
    }

    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.length();
        int m = text2.length();
        vector<vector<int>> dp(n, vector<int>(m, -1));
        return f(n-1, m-1, text1, text2, dp);
    }
```

**TC:** O(n\*m)

**SC:** O(n + m) + O(n\*m)

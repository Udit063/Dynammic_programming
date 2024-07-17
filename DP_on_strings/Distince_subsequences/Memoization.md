# Distinct Subsequence Problem using Memoization Approach

## Approach

In this question, we are given **2 strings** and we need to find the **total subsequences of string 2 in string 1** . So, we will need to find all the subsequences of the string, hence, we will use **recursion** for it.

Since, we need to count no of ways, hence the **base case** should **return 1 or 0** and at last we need to **return the summition**.

For recursion, we will take **2 indexes**, **i for string1** and **j for string2** which will be pointing at the last character of the string. If both **characters matches (Base Case)**, then the **indexes** of both get **reduced to 1** if we take that occurrence, and if we **don't take** that occurrence, only **index of string 1 gets reduced to 1**. But, if the string **characters match**, then keep **j same** and **reduce i** for checking the substring in string 1.

For base case, **if(i < 0)**, means the string doesn't matches, hence **return 0**. and **if(j < 0)**, means the string matches, hence **return 1**. Since, it will create an **overlapping subproblem**, hence, we will use **memoization**.

For memoization, just take a **dp[n][m]** array and store the result in this array. Also, check if any value exists in this array before moving forward.

## Code

```c++
    int f(string s, string t, int i, int j, vector<vector<int>>& dp){
        if(j < 0) return 1;
        if(i < 0) return 0;

        if(dp[i][j] != -1) return dp[i][j];
        if(s[i] == t[j]) return (dp[i][j] = f(s, t, i-1, j-1, dp) + f(s, t, i-1, j, dp));
        else return dp[i][j] = f(s, t, i-1, j, dp);
    }

    int numDistinct(string s, string t) {
        int n = s.length();
        int m = t.length();
        vector<vector<int>> dp(n, vector<int>(m+1, -1));
        return f(s, t, n-1, m-1, dp);
    }
```

**TC:** O(n\*m)

**SC:** O(n + m) + O(n\*m)

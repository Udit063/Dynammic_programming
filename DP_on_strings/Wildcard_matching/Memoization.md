# Wildcard Matching Problem using Memoization Approach

## Approach

In this question, we are given **2 strings** and we need to find that **string1 matches with the string2 with patterns ('\*'/'?')**. **( ? )** matches with the **single character** while **( \* )** matches with the **sequence of length 0 or more**. So, we will need to find all the sequences for **( \* )** to match with the other string, hence, we will use **recursion** for it. For ex, **s = "ab\*cd"** and **p = "abdefcd"**, so, **\* = def** and hence return **true**, as it will match.

For recursion, we will take **2 indexes**, **i for p** and **j for s** which will be pointing at the last character of the string.

Now, we will do **string matching** from the last, if **(p[i] == s[j])** or **(p[i] == '?')**, then means it is **matching**, hence reduce both **(i&j) with 1**. If they **don't match**, then return **false**. But, if we get **(p[i] == '\*')**, then we have to check for **lengths = 0, 1, 2, 3,....**, hence we will use **recursion** for it and check for all conditions, if it takes **0 length** or it takes **1 length** and so on. You can check it by making **recursion tree** also.

For base case, **if(i < 0 && j < 0)**, means both strings ends, hence, return **true**, but if **(j>=0)**, return **false** as string still left for matching. But **if(j<0 && i>=0)** then it will only return **true** if **all characters of p contains '\*'**, otherwise it will return **false**.

Since, it will create an **overlapping subproblem**, hence, we will use **memoization**.

For memoization, just take a **dp[n][m]** array and store the result in this array. Also, check if any value exists in this array before moving forward.

## Code

```c++
    bool f(int i, int j, string p, string s, vector<vector<int>>& dp){
        if(i<0 && j<0) return true;
        if(i<0 && j>=0) return false;
        if(j<0 && i>=0){
            for(int k=0; k<=i; k++){
                if(p[k] != '*') return false;
            }
            return true;
        }

        if(dp[i][j] != -1) return dp[i][j];

        if(p[i] == s[j] || p[i] == '?') return dp[i][j] = f(i-1, j-1, p, s, dp);
        if(p[i] == '*') return dp[i][j] = f(i-1, j, p, s, dp) || f(i, j-1, p, s, dp);

        return dp[i][j] = false;
    }

    bool isMatch(string s, string p) {
        int m = s.size();
        int n = p.size();

        vector<vector<int>> dp(n, vector<int>(m, -1));
        return f(n-1, m-1, p, s, dp);
    }
```

**TC:** O(n\*m)

**SC:** O(n + m) + O(n\*m)

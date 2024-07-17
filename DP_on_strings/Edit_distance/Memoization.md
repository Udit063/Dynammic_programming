# Edit Distance Problem using Memoization Approach

## Approach

In this question, we are given **2 strings** and we need to find the total number of **operations (insert/ delete, replace)** to **convert string 1 to string 2** . So, we will need to find **all possible ways** of each operations to convert the string and give **minimum** of all operations. Hence, we will use **recursion**.

For recursion, we will take **2 indexes**, **i for string1** and **j for string2** which will be pointing at the last character of the string. For this, we will do **string matching** from the last. If the **character matches**, then just reduce both **(i & j) with 1** and check for the next. If it **doesn't match**, then do all the **operations (insert/ delete/ replace)** and **find minimum** of all.

1. **insert:** in insertion in string 1, i will remain same, but j get reduced to check for next.
1. **delete:** in deletion in string 1, i will get reduced by 1, but j will remain same.
1. **replace:** in replacing in string 1, i&j both get reduced by 1.

For base case, **if(i < 0)**, means the **string2 still left**, hence it will **return (j+1) insertion operations** . and **if(j < 0)**, means the **string1 still left**, hence it will **return (i+1) deletion operations**, to convert to string 2. Since, it will create an **overlapping subproblem**, hence, we will use **memoization**.

For memoization, just take a **dp[n][m]** array and store the result in this array. Also, check if any value exists in this array before moving forward.

## Code

```c++
    int f(string word1, string word2, int i, int j, vector<vector<int>>& dp){
        if(i<0) return j+1;
        if(j<0) return i+1;

        if(dp[i][j] != -1) return dp[i][j];

        if(word1[i] == word2[j]) return 0 + f(word1, word2, i-1, j-1, dp);

        int ins = 1 + f(word1, word2, i, j-1, dp);
        int del = 1 + f(word1, word2, i-1, j, dp);
        int rep = 1 + f(word1, word2, i-1, j-1, dp);

        return dp[i][j] = min(ins, min(del, rep));
    }

    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<vector<int>> dp(n, vector<int>(m, -1));

        return f(word1, word2, n-1, m-1, dp);
    }
```

**TC:** O(n\*m)

**SC:** O(n + m) + O(n\*m)

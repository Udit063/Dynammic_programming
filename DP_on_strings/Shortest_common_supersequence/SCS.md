# Shortest common Supersequence Problem using Tabulation Approach

## Approach

In this question, we are given **2 strings** and we have to make **shortest supersequence** such that both strings are the subsequence of that superstring. For ex, **s1 = "brute"** and **s2 = "groot"**, so the shortest supersequence will be **"bgruoote"**. Hence, we can observe the the common characters or **lowest common subsequences** are taken only **once**.

Length of superstring can easily be find by, **length = n + m - len(LCS)**

To find string, we will have to use **dp array** of **lowest common subsequence**. Just look at the table of dp array formed in LCS:-

|     |     |     |   g   |   r   |   o   |   o   |   t   |
| :-: | :-: | :-: | :---: | :---: | :---: | :---: | :---: |
|     |     | #0  |  #1   |  #2   |  #3   |  #4   |  #5   |
|     | #0  |  0  | **0** |   0   |   0   |   0   |   0   |
|  b  | #1  |  0  | **0** |   0   |   0   |   0   |   0   |
|  r  | #2  |  0  |   1   | **1** | **1** |   1   |   1   |
|  u  | #3  |  0  |   1   |   1   | **1** | **1** |   1   |
|  t  | #4  |  0  |   1   |   1   |   1   |   1   | **2** |
|  e  | #5  |  0  |   1   |   1   |   1   |   1   | **2** |

Since, we can see in the table that at **(5,5), (e != t)** , therefore, it come from the **max** of **upper cell** and **left cell**, so if it comes from upper cell **e** will be added to **ans** and move **upwards** and vice-versa. But, if both are same, like **(t == t)**, then it has came from **diagonal** and it will move diagonally after adding _t_ to the **ans once**.

After all the steps, either cell reach on the **top** or **left**, means the other string is still left, so we will add string to the ans.

Also, we are going from down to up, hence **ans** string will be **reversed**.

## Code

```c++
    string shortestCommonSupersequence(string str1, string str2) {
        int n = str1.length();
        int m = str2.length();

        // LCS code
        vector<vector<int>> dp(n+1, vector<int>(m+1, -1));

        for(int ind2=0; ind2<=m; ind2++) dp[0][ind2] = 0;
        for(int ind1=0; ind1<=n; ind1++) dp[ind1][0] = 0;

        for(int ind1 = 1; ind1<=n; ind1++){
            for(int ind2=1; ind2<=m ;ind2++){
                if(str1[ind1-1] == str2[ind2-1]) dp[ind1][ind2] = 1 + dp[ind1-1][ind2-1];
                else dp[ind1][ind2] = max(dp[ind1-1][ind2], dp[ind1][ind2-1]);
            }
        }

        string ans = "";
        int i = n, j = m;
        while(i > 0 && j > 0){
            if(str1[i-1] == str2[j-1]){
                ans += str1[i-1];
                i--;
                j--;
            }
            else if(dp[i-1][j] > dp[i][j-1]){ //upward
                ans += str1[i-1];
                i--;
            }
            else{  // left
                ans += str2[j-1];
                j--;
            }
        }

        while(i > 0) {
            ans += str1[i-1];
            i--;
        }

        while(j > 0) {
            ans += str2[j-1];
            j--;
        }

        reverse(ans.begin(), ans.end());

        return ans;
    }
```

**TC:** O(n\*m)

**SC:** O(n\*m)

# Longest common Subsequence Problem using Space Optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **prev** and **curr** and change accourdingly.

## Code

```c++
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.length();
        int m = text2.length();

        vector<int> prev(m+1, 0), curr(m+1, 0);

        for(int ind2=0; ind2<=m; ind2++) prev[ind2] = 0;

        for(int ind1 = 1; ind1<=n; ind1++){
            for(int ind2=1; ind2<=m ;ind2++){
                if(text1[ind1-1] == text2[ind2-1]) curr[ind2] = 1 + prev[ind2-1];
                else curr[ind2] = max(prev[ind2], curr[ind2-1]);
            }
            prev = curr;
        }
        return prev[m];
    }
```

**TC:** O(n\*m)

**SC:** O(m)

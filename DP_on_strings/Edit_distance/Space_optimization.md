# Edit Distance Problem using Space Optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **prev** and **curr** and change accourdingly.

## Code

```c++
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();

        vector<int> prev(m+1, 0), curr(m+1, 0);

        for(int j=0; j<=m; j++) prev[j] = j;

        for(int i=1; i<=n; i++){
            curr[0] = i;  // base case of (j==0)
            for(int j=1; j<=m; j++){
                if(word1[i-1] == word2[j-1]) curr[j] = 0 + prev[j-1];
                else{
                    int ins = 1 + curr[j-1];
                    int del = 1 + prev[j];
                    int rep = 1 + prev[j-1];

                    curr[j] = min(ins, min(del, rep));
                }
            }
            prev = curr;
        }
        return prev[m];
    }
```

**TC:** O(n\*m)

**SC:** O(m)

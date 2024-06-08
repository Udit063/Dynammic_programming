# Fibonacci Series Through Tabulation approach

## Approach

It is a down-top approach. Instead of recursion call, we declare the base conditions and implement a for loop for the rest and store the values in an array.

## Code

```C++
vector<int>dp1(n+1);
    dp1[0]=0;
    dp1[1]=1;
    for(int i=2;i<=n;i++)
    {
        dp1[i]=dp1[i-1]+dp1[i-2];
    }
    cout<<"tabulation method: "<<dp1[n]<<endl;
```

**Time Complexity** O(n)

**Space Complexity** O(n)

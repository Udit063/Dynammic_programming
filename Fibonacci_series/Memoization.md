# Fibonacci Series Through Memoization DP approach

## Approach

**Memoization is the technique in which values are stored in an array so that we do not have to calculate them again.**

1. Create an array to store the values and initialize with '-1'.
2. Whenever you calculate a value, store it in the array.
3. Before calculating, check if the value already exists in the array (i.e., it is not -1). If it does, return that value.

## Code

```C++
int fib(int n,vector<int> dp)
{
if(n==1 || n==0)
{
return n;
}
if(dp[n]!=-1)
{
return dp[n];
}
dp[n]=fib(n-1,dp)+fib(n-2,dp);
return dp[n];
}
```

**Time Complexity** O(n)

**Space Complexity** O(n)

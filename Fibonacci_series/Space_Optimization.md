# Fibonacci Series Through Space Optimization approach

## Approach

1. Assigned the prev2 and prev for the base conditions and use it for (n-1) and (n-2) elements.
2. Assigned the curr variable that will be the sum of prev and prev2.
3. Now, as we move forward:
   - curr = prev + prev2
   - prev2 = prev
   - prev = curr

## Code

```C++
    int prev2 = 0;
    int prev1 = 1;
    int curr;
    for (int i = 2; i <= n; i++)
    {
        curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }
    cout << "space optimization: " << prev1 << endl;
```

**Time Complexity** O(n)

**Space Complexity** O(1)

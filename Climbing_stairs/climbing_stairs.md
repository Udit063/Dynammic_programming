# Climbing Stairs Problem

## Approach

Since, in this we have to count all the ways to climb the stairs in 1 step or 2 steps then recursion should be applied.

Steps:

1. Try to represent problem in terms of index.
2. Do all possible stuffs on that index according to the problem.
3. Sum up all the stuffs for counting all ways.

For calculating step 1 and step 2, (n-1) and (n-2) will be done respectively for climbing stairs and hence we will find out it is a case of **Fibonacci series**.

## Code

```c++
    int climbStairs(int n) {
        int prev2=0;
        int prev=1;
        int curr;
        for(int i=1;i<=n;i++){
            curr=prev2+prev;
            prev2=prev;
            prev=curr;
        }
        return curr;
    }
```

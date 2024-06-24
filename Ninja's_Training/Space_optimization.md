# Ninja's Training Problem with Space Optimization Approach

## Approach

If we notice, then we can see that we require only the current array and the prev array in the solution. So, we will declare only 2 arrays, one for prev one and 1 for current and rest logic will be same.

## Code

```c++
    int maximumPoints(vector<vector<int>>& points, int n) {
        vector<int> prev(4,0);
        prev[0] = max(points[0][1], points[0][2]);
        prev[1] = max(points[0][0], points[0][2]);
        prev[2] = max(points[0][0], points[0][1]);
        prev[3] = max(points[0][0], max(points[0][1], points[0][2]));

        for(int day=1; day<n; day++){
            vector<int> temp(4,0);         // for current one
            for(int last=0; last < 4; last++){
                temp[last]=0;

                for(int task=0; task<3; task++){
                    if(task != last){
                        int p = points[day][task] + prev[task];
                        temp[last] = max(temp[last], p);
                    }
                }
            }
            prev=temp;
        }
        return prev[3];
    }
```

**TC:** O(n*4*3)

**SC:** O(4)

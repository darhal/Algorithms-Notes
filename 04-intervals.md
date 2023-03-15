# Two Intervals :
- Useful to detect overalapping intervals
- Useful to merge overlapping intervals

Different cases with intervals
```
1) [...A...] 
             [...B...]

2) [...A...] 
       [...B...]

3) [...A...] 
     [.B.]

4)    [...A...] 
   [.B.]

5) [...B...] 
     [.A.]

1) [...B...] 
             [...A...]
```
- If we sort a.start <= b.start => only 1,2 and 3 cases will be possible
- To merge the overlapping intervals (i.e scnearios 2 and 3 after sorting by start)
```
2) [...A...] 
       [...B...]      ---->      C : [A.start .... B.end]

3) [...A...] 
     [.B.]             ---->      C : [A.start .... A.end]
C the merged interval is going to have the following start and end :
c.start = a.start
c.end = max(a.end, b.end)
```

**Example**
```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    vector<vector<int>> merged;
        
    sort(intervals.begin(), intervals.end(), 
    [](const auto& l, const auto& r){
        return l[0] < r[0]; 
    });
        
    int start = intervals[0][0];
    int end = intervals[0][1];
        
    for (int i = 1; i < intervals.size(); i++) {
        auto& interval = intervals[i];
            
        if (interval[0] <= end) { // overlap
            end = max(end, interval[1]);
        }else{
            merged.push_back({start, end});
            start = interval[0];
            end = interval[1];
        }
    }

    // dont forget to push the last interval
    merged.push_back({start, end}); 
    return merged;
}
```
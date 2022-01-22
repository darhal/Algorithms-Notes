# Arrays/Strings :
## Sliding Window : 
- Useful to find the longest/shortest string, subarray or desired value. (Have to be somewhat contigious)
- The window size can shrink or grow depending on the problem

**Note** : Consider prefix sum when the values in the array can be negative

**Useful links** : https://medium.com/leetcode-patterns/leetcode-pattern-2-sliding-windows-for-strings-e19af105316b

**Template :**
```cpp
int max_sum = 0, window_sum = 0; 
/* calculate sum of 1st window */
for (int i = 0; i < k; i++)  
    window_sum += arr[i]; 
/* slide window from start to end in array. */
for (int i = k; i < n; i++){ 
    window_sum += arr[i] - arr[i-k];    // saving re-computation
    max_sum = max(max_sum, window_sum);
}
```

## Prefix Sum :
- The idea is to use an array/matrix of prefix sums/products/etc
- Useful when we are searching for a continuous subarray, sub-matrix or a path in a binary tree/graph

**Link on prefix sum** : https://leetcode.com/problems/path-sum-iii/solution/

## Two pointers :
- Usually used on sorted array
- Two pointers low and high
- Move low and/or high and/to test/satisfy some criteria

## Kadane’s algorithm :
To find a contigious sub-array with the largest sum

**Algorithm template** :
- Initialize:
    - max_so_far = INT_MIN
    - max_ending_here = 0

- Loop for each element of the array
  - max_ending_here = max_ending_here + a[i]
  - if(max_so_far < max_ending_here)
      - max_so_far = max_ending_here
  - if(max_ending_here < 0)
    - max_ending_here = 0
- return max_so_far

**Code template** :
```cpp
int maxSubArray(vector<int>& arr) {
    int n = arr.size();
    int res = arr[0], maxEle = arr[0];
        
    for (int i=1; i<n; i++) {
        maxEle = max(maxEle + arr[i], arr[i]);
        res = max(maxEle, res);
    }
        
    return res;
}
```

## Most frequent element (Boyer-Moore voting algorithm) :
Used to find the most frequent element in the array in O(n) time and O(1) space

**Code template** :
```cpp
int majorityElement(vector<int>& nums) {
    // Boyer-Moore Voting Algorithm
    int candidate = 0;
    int count = 0;
        
    for (int n : nums) {
        if (count == 0) {
            candidate = n;
        }
            
        count += (candidate == n) ? +1 : -1;
    }
        
    return candidate;
}
```

## Cyclic Sort :
- Useful when we have numbers in a certain **range** and asked to find **duplicates** or **missing** ones

**Template :**
```cpp
int start = 0;
        
while (start < nums.size()) {
    int n = nums[start];
    if (n < nums.size() && n != start) {
        swap(nums[start], nums[n]);
    }else{
        start++;
    }
}
```

## Dutch flag problem :
Sort in O(n) time and O(1) space an array of 3 disctinct elements (could be repeated multiple times)

**Template :**
```cpp
// nums can be [2,0,2,1,1,0] or  [2,0,1]
// Output : [0,0,1,1,2,2] and [0,1,2] respectively
void sortColors(vector<int>& nums) {
    int s = 0;
    int e = nums.size() - 1;
        
    for (int i = 0; i <= e;) {
            if (nums[i] == 0)
            swap(nums[s++], nums[i++]);
        else if (nums[i] == 2)
            swap(nums[e--], nums[i]);
        else
            i++;
    }
}
```
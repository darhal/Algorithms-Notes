# Binary Search
Used in a sorted array to find an element

**Ordinary binary search**
```cpp
int binary_search(vector<int>& nums, int target) {
    int pivot, left = 0, right = nums.size() - 1;
    while (left <= right) {
      pivot = left + (right - left) / 2; // avoid overflow
      if (nums[pivot] == target) return pivot;
      if (target < nums[pivot]) right = pivot - 1;
      else left = pivot + 1;
    }
    return -1;
}
```

**How to find the leftmost element**
```cpp
int bs_leftmost(vector<int>& nums, int target) {
    int mid, l = 0, r = nums.size();
    while (l < r) {
        mid = (l+r) / 2;
        if (nums[mid] < target) l = mid + 1;
        else r = mid;
    }
    return l >= 0 && l < nums.size() && nums[l] == target ? l : -1;
}
```

**How to find the rightmost element**
```cpp
int bs_rightmost(vector<int>& nums, int target) {
    int mid, l = 0, r = nums.size();
    while (l < r) {
        mid = (l+r) / 2;
        if (nums[mid] > target) r = mid;
        else l = mid + 1;
    }
    return r-1 >= 0 && r-1 < nums.size() && nums[r-1] == target ? r-1 : -1;
}
```

**How to find the first element in a rotated array**
```cpp
int get_first(vector<int>& nums) {
    int s = 0;
    int e = nums.size() - 1;
        
    while (s < e) {
        int m = s + (e-s)/2;
        if (nums[m] > nums[e]) {
            s = m+1;
        } else {
            e = m;
        }
    }
        
    return s;
}
```

**Binary search in a rotated array**
```cpp
int search(vector<int>& nums, int target) {
    int start = 0, end = nums.length - 1;
    while (start <= end) {
      int mid = start + (end - start) / 2;
      if (nums[mid] == target) 
          return mid;
      else if (nums[mid] >= nums[start]) {
        if (target >= nums[start] && target < nums[mid]) 
            end = mid - 1;
        else 
            start = mid + 1;
      }else {
        if (target <= nums[end] && target > nums[mid]) 
            start = mid + 1;
        else 
            end = mid - 1;
      }
    }
    return -1;
}
```

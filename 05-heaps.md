# Heaps
## Two Heaps
Useful to find a median in a data stream for example :
- Use two heaps (min heap and max heap)
- We can store the smaller part of the list in a max_heap. We are using max_heap because we are only interested in knowing the largest number in the first half of the list.
- We can store the larger part of the list in a min_heap. We are using min_heap because we are only interested in knowing the smallest number in the second half of the list.
- The median of the current list of numbers can be calculated from the top element of the two heaps.
- Inserting a number in a heap will take O(logN) (better than the brute force approach)


An alternative approach chould be using C++ multiset (Which is red-black tree)
- Keep track of the middle element
- Update it upon insertion/deletion

**Example** :
```cpp
vector<double> medianSlidingWindow(vector<int>& nums, int k) {
    vector<double> medians;
    multiset<int> window(nums.begin(), nums.begin() + k);
    auto mid = next(window.begin(), k/2);
    for (int i =k;;i++) {
        // Push the current median
        medians.push_back(((double)(*mid) + *next(mid, k%2-1)) * 0.5); 
        // If all done, break
        if (i == nums.size())
            break;
        // Insert incoming element
        window.insert(nums[i]);
        if (nums[i] < *mid)
            mid--;
        // Remove outgoing element
        if (nums[i-k] <= *mid)
            mid++;
        window.erase(window.lower_bound(nums[i-k]));
    }
    return medians;
}
```

## K-way merge
Useful when we want to merge K sorted linked-lists/arrays
1. We can push the smallest (first) element of each sorted array in a Min Heap to get the overall minimum.
2. After this, we can take out the smallest (top) element from the heap and add it to the merged list.
3. After removing the smallest element from the heap, we can insert the next element of the same list into the heap.
4. We can repeat steps 2 and 3 to populate the merged list in sorted order.

## Top K Numbers
- Find the K'th largest element in an unsorted array
- For each element in the array
    - If element > min_heap.top()
        - min_heap.pop() // Eject smallest element
        - min_heap.push(element) // Push the element bigger than the previous smallest element
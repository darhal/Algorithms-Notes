# C++ :
## Heap
```cpp
priority_queue<T, Container, Compare> heap; // Wrapper that uses heap operations
// if Compare is less<T> then heap is a max heap (less<T> = {lhs < rhs})
// if Compare is greater<T> then heap is a min heap (greater<T> = {lhs > rhs})
// if compare returns true then its first argument will be before its second argument in the heap
// End of the heap is the top of it
heap.top(); // access the top element O(1)
heap.push(element); // push element to the heap O(lgn)
heap.pop(); // remove the top element from the heap O(lgn)
heap.size(); // access the top element O(1)
```
## Stack
```cpp
stack<T> stack;
stack.top(); // top element in the stack
stack.push(element); // push element to the stack
stack.pop(); // Remove top element from the stack
stack.size(); // Returns the size of the stack
```
## Queue
```cpp
queue<T> queue;
queue.push(element); // Add
queue.front(); // First element in the queue (The next element on the list)
queue.pop(); // Remove the front from the queue
queue.back(); // Access last element in the heap
stack.size(); // Returns the size of the queue
```
## set/unordered_set
```cpp
set.insert(element); 
set.erase(element); // erase the element completely from the set
set.count(element); // returns the number of elements matching specific key
set.size(); // How many elements in the set
```
### map
```cpp
auto b = map.begin(); // returns iterator to the smallest element in the map (This is O(1) in C++)
b++; // next bigger element in the list
auto e = map.rbegin(); // returns iterator to the biggest element in the map (This is O(1) in C++)
e--; // next smaller element in the list
```
## Utilities
- prev(itr) -> returns the previous iterator used with end usually
- advance(itr, i) -> advance iterator by i'th element
- Lower and upper bound :
    - std::lower_bound - returns iterator to first element in the given range which is EQUAL_TO or Greater than val.
    - std::upper_bound - returns iterator to first element in the given range which is Greater than val.
    - **Example :** lower_bound(data.begin(), data.end(), i); // Find the lower bound of i in data
    - These functions return data.end() if nothing found
- distance(itr1, itr2) return the distance between two iterators
```
// value a a a b b b c c c
// index 0 1 2 3 4 5 6 7 8
// bound       l     u
// l and u are respectivelly the lower and upper bound of b
```
- nth_element(RandomIt first, RandomIt nth, RandomIt last);
- nth_element is a partial sorting algorithm that rearranges elements in [first, last) such that:
    - The element pointed at by nth is changed to whatever element would occur in that position if [first, last) were sorted.
    - All of the elements before this new nth element are less than or equal to the elements after the new nth element. (Meaning that it puts all elements smaller in the front and all elements larger in the back)
```cpp
std::vector<int> v{5, 10, 6, 4, 3, 2, 6, 7, 9, 3}; 
auto m = v.begin() + v.size()/2;
std::nth_element(v.begin(), m, v.end());
// The median is : v[v.size()/2]
// v is now {3, 2, 3, 4, 5, 6, 10, 7, 9, 6, }
```
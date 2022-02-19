# Heap
```cpp
priority_queue<T, Container, Compare> heap; // Wrapper that uses heap operations
// if Compare is less<T> then heap is a max heap (less<T> = {lhs < rhs})
// if Compare is greater<T> then heap is a min heap (greater<T> = {lhs > rhs})
// if compare returns true then its first argument will be before its second argument in the heap
// End of the heap is the top of it
heap.top(); // access the top element O(1)
heap.push(element); // push element to the heap O(lgn)
heap.pop(); // remove the top element from the heap O(lgn)
heap.size(); // returns the size of the heap
```
# Stack
```cpp
stack<T> stack;
stack.top(); // top element in the stack
stack.push(element); // push element to the stack
stack.pop(); // Remove top element from the stack
stack.size(); // Returns the size of the stack
```
# Queue
```cpp
queue<T> queue;
queue.push(element); // Add
queue.front(); // First element in the queue (The next element on the list)
queue.pop(); // Remove the front from the queue
queue.back(); // Access last element in the queue
stack.size(); // Returns the size of the queue
```
# set/unordered_set
```cpp
set.insert(element); 
set.erase(element); // erase the element completely from the set
set.count(element); // returns the number of elements matching specific key
set.size(); // How many elements in the set
```
## map
```cpp
auto b = map.begin(); // returns iterator to the smallest element in the map (This is O(1) in C++)
b++; // next bigger element in the list
auto e = map.rbegin(); // returns iterator to the biggest element in the map (This is O(1) in C++)
e--; // next smaller element in the list
```
# Utilities
## Lower & upper bound :
`std::lower_bound` : returns iterator to first element in the given range which is EQUAL_TO or Greater than val.

`std::upper_bound` : returns iterator to first element in the given range which is Greater than val.

**Example :** lower_bound(data.begin(), data.end(), i); // Find the lower bound of i in data
**Note :** These functions return data.end() if nothing found
```
// value a a a b b b c c c
// index 0 1 2 3 4 5 6 7 8
// bound       l     u
// l and u are respectivelly the lower and upper bound of b
```
## Iterators :
`std::prev(itr)` -> returns the previous iterator used with end usually

`std::advance(itr, i)` -> advance iterator by i elements

`std::distance(itr1, itr2)` : returns the distance between two iterators

## Nth element (Quick select)
Syntax : `std::nth_element(RandomIt first, RandomIt nth, RandomIt last);`

`nth_element` is a partial sorting algorithm that rearranges elements in [first, last) such that:
- The element pointed at by nth is changed to whatever element would occur in that position if [first, last) were sorted.
- All of the elements before this new nth element are less than or equal to the elements after the new nth element. (Meaning that it puts all elements smaller in the front and all elements larger in the back)

**Example**
```cpp
std::vector<int> v{5, 10, 6, 4, 3, 2, 6, 7, 9, 3}; 
auto m = v.begin() + v.size()/2;
std::nth_element(v.begin(), m, v.end());
// The median is : v[v.size()/2]
// v is now {3, 2, 3, 4, 5, 6, 10, 7, 9, 6, }
```

## Misc :
### Min/Max :
Syntax : `Itr max_element(Itr first, Itr last);`

-> Returns the maximum element in the array/vector.

Syntax : `Itr min_element(Itr first, Itr last);`

-> Returns the minimum element in the array/vector.


Syntax : `std::pair<T&,T&> minmax(T& a, T& b);` 

-> Returns *references* to the smaller and the greater of a and b (respectively).

Syntax : `std::pair<T,T> minmax( std::initializer_list<T> ilist);` 

-> Returns the smallest and the greatest (respectively) of the values in initializer list .

# Hashing
## Fibonacci Hashing
Great article on fibonacci hashing : https://probablydance.com/2018/06/16/fibonacci-hashing-the-optimization-that-the-world-forgot-or-a-better-alternative-to-integer-modulo/

The magic number `0x9e3779b97f4a7c15` comes from `2^64 / phi` where `phi` is the golden ratio
```cpp
template<class T> 
struct std::hash<std::vector<T>> {
    auto operator() (const std::vector<T>& key) const {
        using hasher = std::hash<T>;
        std::size_t seed = key.size();
        for(const auto& i : key) {
            seed ^= hasher{}(i) + 0x9e3779b97f4a7c15 + (seed << 6) + (seed >> 2);
        }
        return seed;
    }
};
````

## To hash types that doesnt support hashing by default
1. Define a hashing function
```cpp
template<class T> 
struct std::hash<T> {
    auto operator() (const T& key) const {
        // Implement a hashing function
        return hash;
    }
};
```
2. Define a compare function
```cpp
bool operator==(const T1& a1, const T2& a2)
{
    // Implementation ...
    return result;
}
```


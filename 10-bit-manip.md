# Bit Manipulation
## XOR
XOR is equal to 0 if the two bits are equal otherwise it's 1
- 0 xor 0 = 0
- 0 xor 1 = 1
- 1 xor 0 = 1
- 1 xor 1 = 0

**Usage :**
- To find a unique number in an array containg duplicates

**Problem Example :**
```cpp
// Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.
int noDup = 0;
for (int n : arr) {
    noDup = noDup ^ n;
}
return noDup;
```
## Popcount
Counts the number of set bits (i.e the number of bits that are set to 1)
```cpp
// C++20
std::popcount(0b011101) // -> 4
std::popcount(8) // -> 1
std::popcount(7) // -> 3
```
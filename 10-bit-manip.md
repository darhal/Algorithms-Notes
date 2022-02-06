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
// C++17 and before
__builtin_popcount(0b011101); // -> 4
```

### Another way to do popcount on software
`n-1` flips the least siginifcant bit of `n` to 0
```
For example:
n         : ...110100
n-1       : ...110011
n & (n-1) : ...110000
```
We keep flipping least siginficant set bits till we reach 0 meaning there is no least significant bits left.
```cpp
int popcount(int n) {
    int sum = 0;
    while (n != 0) {
        sum++;
        n &= (n - 1);
    }
    return sum;
}
```
# Math
## Catalan Number
$$ C_n = \dfrac{1}{n+1}{2n \choose n} = \dfrac{(2n)!}{(n+1)!n!}=\prod_{k=2}^{n}\dfrac{n+k}{k}\quad \text{for } n \ge 0 $$

**Code Example :**
```cpp
// PL : https://leetcode.com/problems/unique-binary-search-trees
// Time: O(N)
// Space: O(1)
class Solution {
public:
    int numTrees(int n) {
        long long ans = 1, i;
        for (i = 1; i <= n; ++i) 
            ans = ans * (i + n) / i;
        return ans / i;
    }
};
```
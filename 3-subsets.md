# Subsets
Useful to get all the elements of the powserset of a given set

## Approach 1
- Start with empty set [ [] ]
- For each element in the array
    - Copy the existing sets in the powerset and add the current element
    - Add the result to the power set

## Approach 2
- Use a bitset to indicate wether an element should be in the powerset or not
- For each element with index i in the given set
    - For j = 0 to 1 << n (where n is the size of the initial set)
        - if ((i >> j) & 1)
            - Add the j'th element into the powerset[i]
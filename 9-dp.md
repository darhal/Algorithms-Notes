# Dynamic Programming
## What is it ?
A paradigm that can explore all possible solutions to a problem. Can solve problems that have the 2 following characteristics : 
- The problem can be broken into overlapping sub-problems (Smaller versions of the original problem that are re-used multiple times)
- The problem has an optimal substructure (Meaning an optimal solution can be formed from optimal solution to the subproblems)

**Not to confuse with :** 
- Greedy problems because they have optimal sub-structure but no overlapping sub-problems
- Divide and conquer because the algorithm break the problem into subproblems but these subproblems are not overlapping

## When to use DP ?
A rule of thumb (not always true) is to look out for these characteristics :
- Common DP problems will ask for optimum value (max, min, shortest, longest), the number of way to do something, if it's possible to reach certain point --> (Greedy or DP).
- Future decisions will depend on earlier decisions. Meaning deciding to do something at one step may affect the ability do something at later step. (This makes greedy algorithm invalid for DP problems)

## The framework
To solve a DP problem we need 3 things :
1. A function or data structure that will compute/contain the answer to the problem for every given state.
2. A recurrence relation to transition between states (Preferbly a mathematical formula).
3. Base cases, so that our recurrence relation doesn't go on infinitely.

## Top-down (Memoization)
Implemented with recursion and made effecient with memoization to avoid unecessary repeated computation (work).

### Steps:
- Visualize the problem as tree
- Figure out a naive recursive solution to the problem
- Figure out the states of the problem
- Before every return statement in the naive solution, store the result of the computation in the memo (hashmap) using current state(s) as a key
- Add a condition at the beginning of the recursive function, if it's in memo then return it immeditely.

### Trade-offs :
- Very easy to write (because ordering of subproblems does not matter)
- Slow due to recursion
- Almost always uses O(N) extra memory because of the implicit call stack (except when tail recusion optimization is applicable)

## Bottom-up (Tabulation)
Implemented with a loop/iteration. Starts at the base case(s) and build the solution up from there.

### Steps:
- Visualize the problem as a table
- Size the table based on the inputs
- Initialize the table with default values 
- Seed the trivial answer into the table (mainly base case)
- Iterate through the table
- Fill further positions based on the current position

### Trade-offs :
- No overhead meaning faster than memoization
- Kinda hard to write correctly
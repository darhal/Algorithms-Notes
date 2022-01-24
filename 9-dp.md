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

## Convert top-down (Recursive) to bottom-up (Iterative)
Steps to convert top-down to bottom-up
1. Do complete top-down implementation
2. Initialize a dp array that is sized according to the state varriable.
    - If there is two states the DP will be 2D array
    - Values in the array should be opposite of what we are searching for (e.g : if we are searching for minimum set values to infinity, if we are searching for max set values to negative infinity)
3. Set the base cases, same as the ones used in the top-down function.
4. Write for loop that iterate over the state variables. Multiple state variables means nested for-loops. Loops should start iterating from the *base cases*.
5. Each iteration of the inner-most loop represents a given state, and is equivalent to a function call to the same state in top-down. Copy the logic from the recursive top-down function into the for-loop and change the function calls to accessing the array. All dp(...) changes into dp[...].
6. dp is now an array populated with the answer to the original problem for all possible states. Return the answer to the original problem by changing return dp(...) to return dp[...].

## Time & Space complexity
DP complexity depends heavily on the number of states of the problem
### Time complexity
If computing each state requires *F* time and there are *n* possible states, then the time complexity is **O(n*F)**

**Example :** If there is 3 state variables 0 <= i <=n  (an integer), 0 <= k <= K (an integer) and holding a boolean, then the time complexity is **O(2nK)** (if *F* is equal to 1)

### Space complexity
Space complexity is also equal to number of states since we store states in both top-down and bottom-up approaches.

**Note :** If calculating a state takes **O(1)** the time and space complexity are the same.

## State Reduction
Sometimes some states can be expressed using other states in the problem. In this case we can eliminate these states to reduce the overall number of states (This is called ***state reduction**).
State reduction usually comes from a clever trick or observation (therefore there is no general rule for them).

When it comes to reducing state variables, it's hard to give any general advice or blueprint. The best advice is to try and think if any of the state variables are related to each other, and if an equation can be created among them. If a problem does not require iteration, there is usually some form of state reduction possible.

**Notes:** 
- State reductions for space complexity usually only apply to bottom-up implementations, while improving time complexity by reducing the number of state variables applies to both implementations.
- Whenever the values calculated by a DP algorithm are only reused a few times and then never used again, check if you can save on space by replacing an array with some variables. A good first step for this is to look at the recurrence relation to see what previous states are used. For example, in Fibonacci, only the previous two states are used, so all results before *n - 2* can be discarded.

## Iteration in the recurrence
Some problems have a static recurrence relation.

For example in Min cost climbind stairs the recurrence relation is : `dp(i)=min(dp(i-1) + cost[i-1], dp(i-2) + cost[i-2])`

Because we are only allowe dto clim 1 or to 2 steps at a time. If the problem changes to be we are allowed to make up to k steps the reccurence relation will become dynamic : 
`dp(i)=min(dp(j) + cost[j]) for all (i-k) ≤ j <i`

**Note:** Usually, static recurrence relations can easily have state reduction. We can also reduce the memory used by only using finite number of variables to represent previous states.

## Counting DP
Counting DP is different than the classical min/max DP. It's reccurance relation usualy looks something like this :
`dp(i) = dp(i-1) + dp(i-2)`.

In counting DP the base case should almost always never be 0 because if its the case we would be adding zeros all the way and the end result will end up also being 0.
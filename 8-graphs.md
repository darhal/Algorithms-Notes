# Graphs
## DFS Iterative
**When to use** : Shortest path

**Algorithm Template:**
```cpp
unordered_set<Node*> visited = {};
stack<Node*> toVisit = { s };

while (toVisist.size()) {
    current = toVisit.top();
    visited.insert(current);

    for (Node* neighbour : current.getNeighbours()) {
        if (visited.count(neighbour ) == 0)
            toVisist.push(neighbour);
    }
}
```

## BFS Iterative : 
**When to use** : Shortest path

**Algorithm Template:**
```cpp
unordered_set<Node*> visited = {};
queue<Node*> toVisit = { s };

while (toVisit.size()) {
    int size = toVisit.size();

    for (int i = 0; i < size; i++) {
        auto current = toVisit.front();
        toVisit.pop();
        visited.insert(current);

        for (Node* neighbour : current.getNeighbours()) {
            if (visited.count(neighbour) == 0)
                toVisit.push(neighbour);
        }
    }

    // This happens each layer
}
```

## Topological sort : 
**When to use** : Dependencies between nodes

### Approach #1 : Algorithm (using BFS) :
```cpp
vector<Node*> sorted;
queue<Node*> toVisit;
// Push all nodes with incoming degree of 0 to toVisit

while (toVisit()) {
    Node* curr = toVisit.front();
    toVisit.pop();
    sorted.emplace_back(curr);

    for (Node* next : curr.getNeighbors()) {
        if (--inDegrees[next] == 0) {
            toVisit.push(next);
        }
    }
}

// If sorted.size() ==  to the number of the nodes in the graph ⇒ then there is no cycle
```

### Approach #2 : Algorithm (using DFS) :
- Apply normal DFS
- When popping from the dfs stack, add these elements to a list
- Reverse the list
- List should contain the nodes in their topological order
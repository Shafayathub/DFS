# Depth-First Search (DFS) in C++

## Introduction
**Depth-First Search (DFS)** is a graph traversal algorithm that explores as far as possible along a branch before backtracking. It uses a **stack (LIFO)** approach, either explicitly with a data structure or implicitly via recursion.

## Properties of DFS
- Works for both **graph** and **tree** traversal.
- Uses **stack (LIFO)** for traversal.
- **Time Complexity:** O(V + E) (where V = vertices, E = edges)
- **Space Complexity:** O(V) (for storing visited nodes and recursive calls)

## DFS Algorithm
1. Start from a source node.
2. Mark the node as visited.
3. Process the node.
4. Recursively visit all unvisited adjacent nodes.

## DFS Implementation in C++

### DFS Using Recursion (Adjacency List Representation)
```cpp
#include <iostream>
#include <vector>
using namespace std;

void dfsHelper(int node, vector<int> adj[], vector<bool> &visited) {
    visited[node] = true;
    cout << node << " ";
    
    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfsHelper(neighbor, adj, visited);
        }
    }
}

void dfs(int start, vector<int> adj[], int V) {
    vector<bool> visited(V, false);
    dfsHelper(start, adj, visited);
}

int main() {
    int V = 5;
    vector<int> adj[V];
    adj[0] = {1, 2};
    adj[1] = {0, 3, 4};
    adj[2] = {0, 4};
    adj[3] = {1};
    adj[4] = {1, 2};
    
    cout << "DFS starting from node 0: ";
    dfs(0, adj, V);
    return 0;
}
```

### DFS Using Stack (Iterative)
```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

void dfsIterative(int start, vector<int> adj[], int V) {
    vector<bool> visited(V, false);
    stack<int> s;
    s.push(start);
    
    while (!s.empty()) {
        int node = s.top();
        s.pop();
        
        if (!visited[node]) {
            visited[node] = true;
            cout << node << " ";
            
            for (auto it = adj[node].rbegin(); it != adj[node].rend(); ++it) {
                if (!visited[*it]) {
                    s.push(*it);
                }
            }
        }
    }
}
```

## DFS Applications
- **Path Finding** (Maze solving, AI in games)
- **Topological Sorting** (Ordering of tasks in scheduling problems)
- **Cycle Detection** (Detecting cycles in a directed or undirected graph)
- **Connected Components** (Finding all connected subgraphs in an undirected graph)
- **Solving Puzzles** (Such as Sudoku solvers)

## DFS vs BFS
| Feature | DFS | BFS |
|---------|----|----|
| Data Structure | Stack (Recursion/LIFO) | Queue (FIFO) |
| Traversal Order | Depth-wise | Level-wise |
| Space Complexity | O(V) (recursive stack) | O(V) |
| Finds Shortest Path? | No | Yes (for unweighted graphs) |
| Suitable for? | Pathfinding, cycles, topological sorting | Shortest paths, connectivity |

## Additional Resources
- [DFS Algorithm (GeeksforGeeks)](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)
- [DFS Explanation (YouTube)](https://www.youtube.com/watch?v=7fujbpJ0LB4)

---
📌 *This file serves as a quick revision guide for DFS in C++. Feel free to contribute or suggest improvements!* 🚀
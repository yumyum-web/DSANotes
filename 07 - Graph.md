# Graph

## Introduction

- Graph is a non-linear data structure that consists of nodes and edges.

## Terminology

### Basic Definitions

- **$V$** = Set of vertices.
- **$E$** = Set of edges.
- **$G = (V, E)$** = Graph.

### Properties of Vertices and Edges

- **Adjacent**: Two vertices are adjacent if there is an edge between them.
- **Incident**: An edge is incident to a vertex if the edge is connected to the vertex.
- **Degree of a Vertex**: Number of edges incident to a vertex.
- **In-degree of a Vertex**: Number of edges coming into a vertex.
- **Out-degree of a Vertex**: Number of edges going out of a vertex.

### Types of Graphs

- **Undirected Graph**: Graph where edges have no direction.
- **Directed Graph**: Graph where edges have direction.
- **Weighted Graph**: Graph where edges have weights.

### Paths and Cycles

- **Path**: A sequence of vertices where each adjacent pair is connected by an edge.
- **Cycle**: A path where the first and last vertices are the same.
- **Simple Path**: A path where no vertex is repeated, i.e., no cycles.
- **Path cost**: Sum of the edge weights in the path.
- **Path Length**: Number of edges in the path.
- **Shortest Path**: A path with the minimum path cost.
- **Reachable**: A vertex is reachable from another vertex if there is a path between them.

### Special Graphs

- **Dense Graph**:
    - A graph where the number of edges is close to the maximum possible edges.
    - When $|E| \approx |V|^2$
- **Sparse Graph**:
    - A graph where the number of edges is much less than the maximum possible edges.
    - When $|E| << |V|^2$
- **Complete Graph**: A graph where an edge connects every pair of vertices.
    - Then $|E| = |V| \times (|V| - 1) / 2$
- **Connected Graph**: A graph where there is a path between every pair of vertices.
    - Then $|E| \geq |V| - 1$
- **Strongly Connected Graph**: A _directed_ graph where there is a path between every pair of vertices.
- **Tree**: A connected graph with no cycles.
    - Then $|E| = |V| - 1$

### Properties of Graphs

- **Cost of a Graph**: Sum of all the edge weights in the graph.

### Subgraphs

- **Subgraph**: A graph whose vertices and edges are subsets of another graph.
- **Spanning Subgraph**: A subgraph that contains all the vertices of the original graph.
- **Spanning Tree**: A spanning subgraph that is a tree.

## Graph Representation

### Adjacency List

- The graph is represented as an array of linked lists.
- Each element in the array represents a vertex. The list contains the vertices adjacent to the vertex.
- Space complexity: $O(V + E)$
- Suitable for sparse graphs.
- Searching for an edge between two vertices: $\Theta(deg(v))$
    - $O(V)$ for worst case.

```cpp
class Graph {
private:
    int V;
    vector<vector<int>> adj;
public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }
};
```

### Adjacency Matrix

- The graph is represented as a 2D array.
- The value at `matrix[u][v]` is `1` if there is an edge between `u` and `v`, otherwise `0`.
- This bit value can be replaced with the weight of the edge.
- Space complexity: $O(V^2)$
- Suitable for dense graphs.
- Searching for an edge between two vertices: $\Theta(1)$

```cpp
class Graph {
private:
    int V;
    vector<vector<int>> matrix;
public:
    Graph(int V) {
        this->V = V;
        matrix.resize(V, vector<int>(V, 0));
    }

    void addEdge(int u, int v) { // Weight specified as third argument
        matrix[u][v] = 1;
        matrix[v][u] = 1; // For undirected graph
    }
};
```

## Searching in Graphs

- Searching in graphs is for understanding the structure of the graph.
- **Depth-First Search (DFS)**: Traverses the graph by going as deep as possible.
- **Breadth-First Search (BFS)**: Traverses the graph level by level.
- **The order of traversing children and the starting vertex can vary based on the use case.**

### Breadth-First Search (BFS)

- BFS traverses the graph level by level.
- Input:
    - The graph.
    - The starting vertex.
- Output:
    - Distances from the starting vertex to all other vertices.
    - Predecessor of each vertex.
- BFS is implemented using a queue.
- Can be used to find the shortest path in an unweighted graph.

#### Algorithm

1. Create a queue and push the starting vertex.
2. Mark the starting vertex as visited.
3. While the queue is not empty:
    - Pop the front vertex.
    - Add the vertex to the result.
    - For each adjacent vertex:
        - If the vertex is not visited:
            - Push the vertex to the queue.
            - Mark the vertex as visited.

- Time complexity: $O(V + E)$

```cpp
vector<int> bfs(int V, vector<vector<int>> adj, int start) {
    vector<int> visited(V, false); // This takes O(V)
    vector<int> result;
    queue<int> q;
    q.push(start);
    visited[start] = true;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        result.push_back(u);
        for (int v: adj[u]) { // This takes O(E)
            if (!visited[v]) {
                q.push(v);
                visited[v] = true;
            }
        }
    }
    return result;
}
```

- The **predecessor** of a vertex is the vertex from which that vertex was visited.
- **Predecessor Subgraph**: The graph formed by the predecessors from the BFS traversal.

#### Breadth-First Tree

- The BFS traversal forms a tree called the **Breadth-First Tree**.
- The tree is rooted at the starting vertex.
- The tree represent the order in which the vertices are visited during BFS.
    - The parent of a vertex is the vertex from which it was visited.
- The tree is the **shortest path tree** if the graph is unweighted.

### Depth-First Search (DFS)

- DFS traverses the graph by going as deep as possible before backtracking.
- Input:
    - The graph.
- Output:
    - Discovery and finishing times of each vertex.
    - Predecessor of each vertex.
- DFS is implemented using recursion or a stack.
- Can be used to find the connected components in a graph.

#### Algorithm

1. Create a stack and push the starting vertex.
2. Mark the starting vertex as visited.
3. While the stack is not empty:
    - Pop the top vertex.
    - Add the vertex to the result.
    - For each adjacent vertex:
        - If the vertex is not visited:
            - Push the vertex to the stack.
            - Mark the vertex as visited.

- Time complexity: $O(V + E)$

```cpp
vector<int> dfsVisit(int V, vector<vector<int>> adj, int start) {
    vector<int> visited(V, false); // This takes O(V)
    vector<int> result;
    stack<int> s;
    s.push(start);
    visited[start] = true;
    while (!s.empty()) {
        int u = s.top();
        s.pop();
        result.push_back(u);
        for (int v: adj[u]) { // This takes O(E)
            if (!visited[v]) {
                s.push(v);
                visited[v] = true;
            }
        }
    }
    return result;
}
```

#### Parenthesis Theorem

- Parenthesis theorem states how the time period between the discovery and finishing of two vertices can overlap.
- **d**: Discovery times of vertices.
- **f**: Finishing times of vertices.
- **Theorem**: For any two vertices $u$ and $v$ exactly one of the following holds:

| Condition                   | Explanation                                                       | verdict                                   |
|-----------------------------|-------------------------------------------------------------------|-------------------------------------------|
| $d[u] < d[v] < f[v] < f[u]$ | Vertex $v$ was discovered during the time $u$ was being explored. | Vertex $v$ is a descendant of vertex $u$. |
| $d[v] < d[u] < f[u] < f[v]$ | Vertex $u$ was discovered during the time $v$ was being explored. | Vertex $u$ is a descendant of vertex $v$. |
| $d[u] < f[u] < d[v] < f[v]$ | Vertex $u$ was discovered and finished before $v$ was discovered. | Both vertices are independent.            |

> **Corollary**: If $u$ is a proper descendant of $v$, then $d[v] < d[u] < f[u] < f[v]$.
>
> **Proper Descendant**: A vertex $u$ is a proper descendant of $v$ if $u$ is a descendant of $v$ and $u \neq v$.

#### Depth-First Forest

- The DFS traversal forms a forest called the **Depth First Forest**.
- This forest represents the connected components in the graph.
- This forest is a collection of **spanning trees** of the connected components.
- Used to identify the ancestor-descendant relationships in a graph.

#### White path theorem

- **White Vertex**: A vertex that has not been visited.
- **Gray Vertex**: A vertex that has been visited but not finished.
- **Black Vertex**: A vertex that has been visited and finished.
- For vertex $u$ to be a descendant of vertex $v$, When $v$ is discovered, there is a white path from $v$ to $u$.

#### Classification of Edges

- **Tree Edge**:
    - An edge that is part of the depth-first tree.
    - An edge from a gray vertex to a white vertex.
- **Back Edge**:
    - An edge that connects a vertex to an ancestor.
    - An edge from a gray vertex to a gray vertex.
    - Indicates a cycle in the graph.
- **Forward Edge**:
    - An edge that connects a vertex to a descendant.
    - An edge from a gray vertex to a descendant black vertex.
- **Cross Edge**:
    - An edge that connects two vertices that are not ancestor-descendant.
    - An edge from a gray vertex to a black vertex that is not a descendant.

## Minimum Spanning Tree (MST)

- A MST is a spanning tree with the **minimum cost.**
- **Cost of a Spanning Tree**: Sum the edge weights in the tree.
- Created from a connected, weighted, undirected graph.
- MST is unique when the weights of the edges are unique, i.e., no two edges have the same weight.

<img alt="MST Example" src="images/MST example.png">

### Steiner Minimum Tree

- A Steiner Minimum Tree is a tree that connects a subset of vertices in a graph.
- The tree is a minimum spanning tree for the subset of vertices.
- Created from a connected, weighted, undirected graph.
- **Terminal Vertices**: Vertices that must be included in the Steiner Minimum Tree.
- **Steiner Vertices**: Vertices that are not terminal vertices.

### Generic Algorithm

1. Maintain a subset of edges A that are part of the MST.
    - Initially, A is empty.
2. While A does not form a spanning tree:
    - Add a safe edge to A.

#### Safe Edge

- An edge is **safe** if it can be added to the MST without violating the property of the MST.
- **Cut**: A partition of the vertices into two disjoint sets.
- An **edge crosses a cut** if one of its endpoints is in one set and the other endpoint is in the other set.
- A cut **respects a set of edges** if no edge in the set crosses the cut.
- **Light Edge**: An edge that is the minimum weight edge that crosses a cut.

1. Let $G = (V, E)$ be a connected, undirected graph with a weight function $w: E \to \mathbb{R}$.
2. Let $A$ be a subset of $E$ that is included in some MST of $G$.
3. Let $C = (S, V - S)$ be any cut that respects $A$.
4. Let $(u, v)$ be a light edge crossing $C$.
5. Then, $(u, v)$ is safe for $A$.

### Kruskal's Algorithm

- Kruskal's algorithm is a greedy algorithm to find the MST.
- The algorithm adds the lightest edge that does not form a cycle in the MST.
- The algorithm uses a **disjoint set** data structure to detect cycles.
    - **Disjoint Set**: A data structure that keeps track of a set of elements partitioned into a number of disjoint
      subsets.
    - Keep track of each element's parent and the rank of each subset.
- It is a greedy algorithm because it chooses the locally optimal solution by selecting the lightest edge.
- Suitable for **sparse** graphs.

#### Steps

1. Sort the edges by weight.
2. Initialize an empty MST.
3. For each edge $(u, v)$ in the sorted edges:
    - If the edge is between two disjoint sets:
        - Add the edge to the MST.
        - Merge the two sets.

- Time complexity: $O(E \log E)$

#### Implementation

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class DisjointSet {
private:
    vector<int> parent;
    vector<int> rank;
public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }

    int find(int u) {
        if (parent[u] == u) {
            return u;
        }
        return parent[u] = find(parent[u]);
    }

    void merge(int u, int v) {
        int pu = find(u);
        int pv = find(v);
        if (pu != pv) {
            if (rank[pu] < rank[pv]) {
                parent[pu] = pv;
            } else if (rank[pu] > rank[pv]) {
                parent[pv] = pu;
            } else {
                parent[pu] = pv;
                rank[pv]++;
            }
        }
    }
};

vector<pair<int, pair<int, int>>> kruskal(int V, vector<pair<int, pair<int, int>>> edges) {
    sort(edges.begin(), edges.end());
    DisjointSet ds(V);
    vector<pair<int, pair<int, int>>> mst;
    for (auto edge: edges) {
        int u = edge.second.first;
        int v = edge.second.second;
        if (ds.find(u) != ds.find(v)) {
            mst.push_back(edge);
            ds.merge(u, v);
        }
    }
    return mst;
}
```

### Prim's Algorithm

- Prim's algorithm is a greedy algorithm to find the MST.
- The algorithm adds the lightest edge that connects the MST to a new vertex.
- The algorithm uses a **priority queue** to find the lightest edge.
- It is a greedy algorithm because it chooses the locally optimal solution by selecting the lightest edge.
- Suitable for **dense** graphs.

#### Steps

1. Initialize an empty MST.
2. Initialize a priority queue with the starting vertex.
3. While the priority queue is not empty:
    - Pop the lightest edge.
    - Add the edge to the MST.
    - Add the adjacent vertices to the priority queue.

#### Implementation

```cpp
#include <vector>
#include <queue>

using namespace std;

vector<pair<int, pair<int, int>>> prim(int V, vector<vector<pair<int, int>>> adj) {
    vector<pair<int, pair<int, int>>> mst;
    vector<bool> visited(V, false);
    priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<>> pq;
    pq.push({0, {0, 0}});
    while (!pq.empty()) {
        auto [weight, edge] = pq.top();
        pq.pop();
        int u = edge.first;
        int v = edge.second;
        if (visited[v]) continue;
        visited[v] = true;
        if (u != v) mst.push_back({weight, {u, v}}); // Skip the fake edge {0, 0}
        for (auto [neighbor, w]: adj[v]) {
            if (!visited[neighbor]) {
                pq.push({w, {v, neighbor}});
            }
        }
    }
    return mst;
}
```

## Single Source Shortest Path

- Single source shortest path algorithms find the shortest path from a single source vertex to all other vertices.
- Applicable to _weighted_ and _directed_ graphs.
    - Doesn't have to be connected (Unreachable vertices will have infinite distance).
    - Can be cyclic.
    - Can have negative weights.
    - Can't have negative cycles that are reachable from the source vertex.
- Properties of the shortest path:
    - **Optimal Substructure**: The shortest path between two vertices contains the shortest path between the
      intermediate vertices.
    - **No Cycles**
    - **Greedy Choice**: The shortest path is the sum of the shortest path to the previous vertex and the weight of the
      edge to the next vertex.
    - **Triangle Inequality**: The shortest path between two vertices is less than or equal to the sum of the shortest
      paths between the vertices and an intermediate vertex.

### Relaxation

- **Relaxation**: The process of updating the shortest path to a vertex if a shorter path is found.
- In relaxation the distance to vertices and the predecessor of the vertices are kept track of.

#### Initialize

1. Set the distance of the source vertex to 0.
2. Set the distance of all other vertices to infinity.
3. Set the predecessor of all vertices to null.

#### Relax

1. For an edge $(u, v)$:
    - If $dist[u] + weight(u, v) < dist[v]$:
        - $dist[v] = dist[u] + weight(u, v)$
        - $pred[v] = u$

### Bellman-Ford Algorithm

- Uses dynamic programming.
- **Dynamic Programming**: Solves a problem by breaking it down into simpler overlapping subproblems.
- Supports negative weights. (Can detect negative cycles)
- Not suitable for dense or large graphs.

#### Steps

1. Initialize the distance of the source vertex to 0.
2. Initialize the distance of all other vertices to infinity.
3. Relax all edges $|V| - 1$ times.
4. Check for negative cycles by relaxing all edges one more time.
5. The shortest path is the distance to the vertices.
6. The predecessor of the vertices can be used to find the path.

- Time complexity: $O(V \cdot E)$

#### Implementation

```cpp
#include <vector>

using namespace std;

vector<int> bellmanFord(int V, vector<vector<pair<int, int>>> adj, int start) {
    vector<int> dist(V, INT_MAX);
    vector<int> pred(V, -1);
    dist[start] = 0;
    for (int i = 0; i < V - 1; i++) {
        for (int u = 0; u < V; u++) {
            for (auto [v, w]: adj[u]) {
                if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                    pred[v] = u;
                }
            }
        }
    }
    for (int u = 0; u < V; u++) {
        for (auto [v, w]: adj[u]) {
            if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
                cout << "Negative cycle detected" << endl;
                return {};
            }
        }
    }
    return dist;
}
```

### Dijkstra's Algorithm

- **Greedy Algorithm**: Chooses the locally optimal solution at each step.
- Assumes non-negative weights (So it can't detect negative cycles).
    - This is because the algorithm doesn't revisit vertices and assumes paths can only get longer.
- Suitable for dense graphs.

#### Steps

1. Initialize the distance of the source vertex to 0.
2. Initialize the distance of all other vertices to infinity.
3. Initialize a priority queue with the starting vertex.
4. While the priority queue is not empty:
    - Pop the vertex with the minimum distance.
    - Relax the edges of the vertex.
    - Add the adjacent vertices to the priority queue.

- Time complexity: $O(V \log V + E)$

#### Implementation

```cpp
#include <vector>
#include <queue>

using namespace std;

vector<int> dijkstra(int V, vector<vector<pair<int, int>>> adj, int start) {
    vector<int> dist(V, INT_MAX);
    vector<int> pred(V, -1);
    dist[start] = 0;
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
    pq.push({0, start});
    while (!pq.empty()) {
        auto [d, u] = pq.top();
        pq.pop();
        for (auto [v, w]: adj[u]) {
            if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pred[v] = u;
                pq.push({dist[v], v});
            }
        }
    }
    return dist;
}
```

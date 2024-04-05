---
description: Used on connected undirected graph
---

# Minimum Spanning Tree(MST)

### Generic method

* A is a set of edges that is a part of MST.

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Kruskal

* Using Union-Find
* Sort the edges in non-decreasing order and check if it is safe to add using set and union
* Time complexity = O(E log(E)) or O(E log(V)) as |E| <= |V|^2.
* Space = O(V + E).

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Prim's

* This technique is used in Dijkstra's algorithm as well.
* Start from a node, call it the root node.
* Update the distance of all vertices connected to the current node.
* Pick the vertex with the least distance and still not included in MST set.
* Time complexity = O(V^2) which can be further reduced to O(E log(V)) using min-heap and heapify after each extraction of the top.

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

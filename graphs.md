<!-- SPDX-License-Identifier: CC0-1.0 -->

# Some Graph Algorithms

## Basic Traversals

1. DFS

2. BFS

## Cycle Detection and Topological Sorting

1. Cycle detection by DFS.

2. Topological sorting by DFS (with and without cycle checking).

3. Topological sorting by Kahn's algorithm.

4. Cycle detection by Kahn's algorithm.

## Single-Source Shortest Paths

1. In a tree - O(V + E):

   The path is unique, so just traverse the tree in any way -- such as DFS or
   BFS -- to find it.

2. In an unweighted graph, or with all-equal positive weights - O(V + E):

   BFS.

3. In a DAG - O(V + E):

   Topologically sort (linearize) the DAG. Then relax all edges in linearized
   order of their source vertices.

   The topological sorting can be done as a separate step, or it can be
   interleaved with the process of relaxing the edges and building the shortest
   paths tree. (This is the case both with DFS toposort and Kahn's algorithm.)

4. In any graph - O(V*E):

   Bellman-Ford.

   This can be made to detect and report negative-weight cycles. The first
   |V - 1| passes may continue improving the paths found in the absence of
   negative-weight cycles. If a |V|th pass is done and anything changes, there
   is a negative-weight cycle.

5. In a graph whose weights are all nonnegative - running time varies by PQ:

   Dijkstra's algorithm.

   With an unordered priority queue (array or hash table) - O(V^2)

   With a binary heap - O((V + E) log V)

   After implementing those, also at least discuss d-ary heaps.

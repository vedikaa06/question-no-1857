# question-no-1857
Solution to the question no 1857 on leet code 

1857. Largest Color Value in a Directed Graph
There is a directed graph of n colored nodes and m edges. The nodes are numbered from 0 to n - 1.

You are given a string colors where colors[i] is a lowercase English letter representing the color of the ith node in this graph (0-indexed). You are also given a 2D array edges where edges[j] = [aj, bj] indicates that there is a directed edge from node aj to node bj.

A valid path in the graph is a sequence of nodes x1 -> x2 -> x3 -> ... -> xk such that there is a directed edge from xi to xi+1 for every 1 <= i < k. The color value of the path is the number of nodes that are colored the most frequently occurring color along that path.

Return the largest color value of any valid path in the given graph, or -1 if the graph contains a cycle.

The code uses Depth-First Search (DFS) with dynamic programming to find the longest path with the most occurrences of a single color.

count[node][c] stores the maximum frequency of character c found on any path ending at node.
vis array tracks visited states:
0: Not visited
1: Currently visiting (in recursion stack - indicates a cycle)
2: Visited and processed
The dfs function works as follows:

Cycle Detection: If vis[node] is 1, a cycle is detected, so it returns INF (indicating an invalid path).
Memoization: If vis[node] is 2, it means this node has already been processed, so its pre-calculated count value for its own color is returned.
Explore Neighbors: It recursively calls dfs for all neighbors.
Update Counts: After visiting a neighbor nxt, count[node][c] is updated to be the maximum of its current value and count[nxt][c] for all colors c. This propagates the maximum color counts from downstream nodes.
Add Current Node's Color: count[node] for the current node's color is incremented.
Mark Processed: vis[node] is set to 2 after processing.
Return: Returns the count of the current node's color at this node.
The largestPathValue function:

Initializes the adjacency list, count array, and vis array.
Iterates through all nodes, calling dfs for each.
ans keeps track of the maximum path value found so far.
If ans remains INF after all DFS calls, it means a cycle was detected, so it returns -1. Otherwise, it returns ans.

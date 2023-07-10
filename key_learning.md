# Graph 
- For BFS, need to mark visited before enqueue, otherwise, the same node will be enqueued multiple times

- For any shortest path problem, use BFS with level traversal. Level traversal is the key, otherwise, when marking some cell as visited, we might block way from some cell to reach the destination.
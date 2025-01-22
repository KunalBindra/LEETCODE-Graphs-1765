# LEETCODE-Graphs-1765
This code snippet implements a solution to calculate the highest peak matrix for a given `isWater` matrix. Let's break it down:

### **Problem Understanding**
The `isWater` matrix has the following rules:
- `isWater[i][j] == 1`: The cell `(i, j)` is water.
- `isWater[i][j] == 0`: The cell `(i, j)` is land.

The task is to assign each land cell a height such that:
1. The height of a water cell is `0`.
2. Heights of land cells are minimized, with the constraint that the height of a cell is at least 1 greater than its neighboring cells (if possible).

### **Solution Details**
1. **Initialization:**
   - The `height` matrix is initialized to `-1` for all cells except water cells, which are initialized to `0`.
   - A queue (`que`) is used to perform a Breadth-First Search (BFS). All water cells `(i, j)` with `isWater[i][j] == 1` are added to the queue initially, serving as the starting points.

2. **BFS Approach:**
   - BFS is performed using the queue, processing cells level by level.
   - For each cell `(i, j)` in the queue:
     - Explore its four neighbors (`up`, `down`, `left`, `right`) using the `directions` array.
     - If a neighbor is within bounds and has not been assigned a height (`height[i_][j_] == -1`), update its height as `height[i_][j_] = height[i][j] + 1` and add it to the queue.

3. **Return Result:**
   - After the BFS completes, the `height` matrix contains the desired heights.

### **Key Points**
- **Complexity:**
  - **Time Complexity:** \(O(m \times n)\), where \(m\) is the number of rows and \(n\) is the number of columns. Each cell is visited once.
  - **Space Complexity:** \(O(m \times n)\), due to the `height` matrix and the queue.
  
- **Correctness:**
  - The BFS ensures that the height of a land cell is calculated based on the shortest path to the nearest water cell, satisfying the constraints.

### **Example Dry Run**
For `isWater = [[0,1],[0,0]]`:
- Initialize:
  ```
  height = [[-1, 0],
            [-1, -1]]
  ```
  Queue: `[[0, 1]]`

- BFS Iteration 1:
  - Process `(0,1)`: Update neighbors `(0,0)` and `(1,1)` to height `1`.
  ```
  height = [[1, 0],
            [-1, 1]]
  ```
  Queue: `[[0,0], [1,1]]`

- BFS Iteration 2:
  - Process `(0,0)`: Update neighbor `(1,0)` to height `2`.
  ```
  height = [[1, 0],
            [2, 1]]
  ```
  Queue: `[[1,1], [1,0]]`

- BFS Iteration 3:
  - Process `(1,1)` and `(1,0)`: No further updates needed.

Final Output:
```
[[1, 0],
 [2, 1]]
```

The code is correct and efficient for the given problem.

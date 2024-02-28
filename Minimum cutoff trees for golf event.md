# Cut Off Trees for Golf Event

## Problem Description

You are asked to cut off all the trees in a forest for a golf event. The forest is represented as an m x n matrix. In this matrix:

- 0 means the cell cannot be walked through.
- 1 represents an empty cell that can be walked through.
- A number greater than 1 represents a tree in a cell that can be walked through, and this number is the tree's height.

In one step, you can walk in any of the four directions: north, east, south, and west. If you are standing in a cell with a tree, you can choose whether to cut it off.

You must cut off the trees in order from shortest to tallest. When you cut off a tree, the value at its cell becomes 1 (an empty cell).

Starting from the point (0, 0), return the minimum steps you need to walk to cut off all the trees. If you cannot cut off all the trees, return -1.

### Example 1:

Input: 
```
forest = [[1,2,3],
          [0,0,4],
          [7,6,5]]
```
Output: 
```
6
```
Explanation: 
Following the path above allows you to cut off the trees from shortest to tallest in 6 steps.

### Example 2:

Input: 
```
forest = [[1,2,3],
          [0,0,0],
          [7,6,5]]
```
Output: 
```
-1
```
Explanation: 
The trees in the bottom row cannot be accessed as the middle row is blocked.

### Example 3:

Input: 
```
forest = [[2,3,4],
          [0,0,5],
          [8,7,6]]
```
Output: 
```
6
```
Explanation: 
You can follow the same path as Example 1 to cut off all the trees. Note that you can cut off the first tree at (0, 0) before making any steps.

## Solution Code

```java
import java.util.*;

class Solution {
    public int cutOffTree(List<List<Integer>> forest) {
        if (forest == null || forest.size() == 0 || forest.get(0).size() == 0)
            return -1;

        List<int[]> trees = new ArrayList<>();
        int m = forest.size();
        int n = forest.get(0).size();

        // Collect all trees
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int height = forest.get(i).get(j);
                if (height > 1)
                    trees.add(new int[]{i, j, height});
            }
        }

        // Sorting trees based on height
        Collections.sort(trees, (a, b) -> a[2] - b[2]);

        int totalSteps = 0;
        int startX = 0, startY = 0;

        // Traversing through the trees in sorted order
        for (int[] tree : trees) {
            int steps = bfs(forest, startX, startY, tree[0], tree[1]);
            if (steps == -1) // If any tree cannot be reached, return -1
                return -1;
            totalSteps += steps;
            startX = tree[0];
            startY = tree[1];
        }

        return totalSteps;
    }

    // Breadth-first search to find the shortest path from (startX, startY) to (targetX, targetY)
    private int bfs(List<List<Integer>> forest, int startX, int startY, int targetX, int targetY) {
        int m = forest.size();
        int n = forest.get(0).size();
        boolean[][] visited = new boolean[m][n];
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{startX, startY, 0});
        visited[startX][startY] = true;

        int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            int x = curr[0];
            int y = curr[1];
            int steps = curr[2];

            if (x == targetX && y == targetY)
                return steps;

            for (int[] dir : dirs) {
                int newX = x + dir[0];
                int newY = y + dir[1];
                if (newX >= 0 && newX < m && newY >= 0 && newY < n && !visited[newX][newY] && forest.get(newX).get(newY) > 0) {
                    visited[newX][newY] = true;
                    queue.offer(new int[]{newX, newY, steps + 1});
                }
            }
        }

        return -1; // If target cannot be reached
    }
}
```

This code provides a solution to the problem using Breadth-First Search (BFS) to find the shortest path from the starting point to each tree.

# Snakes and Ladders

## Problem Description

You are given an n x n integer matrix `board` where the cells are labeled from 1 to n^2 in a Boustrophedon style starting from the bottom left of the board (i.e. `board[n - 1][0]`) and alternating direction each row.

You start on square 1 of the board. In each move, starting from square `curr`, do the following:

1. Choose a destination square `next` with a label in the range `[curr + 1, min(curr + 6, n^2)]`. This choice simulates the result of a standard 6-sided die roll: i.e., there are always at most 6 destinations, regardless of the size of the board.
2. If `next` has a snake or ladder, you must move to the destination of that snake or ladder. Otherwise, you move to `next`.

The game ends when you reach the square `n^2`.

A board square on row `r` and column `c` has a snake or ladder if `board[r][c] != -1`. The destination of that snake or ladder is `board[r][c]`. Squares 1 and `n^2` do not have a snake or ladder.

Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do not follow the subsequent snake or ladder.

Return the least number of moves required to reach the square `n^2`. If it is not possible to reach the square, return -1.

### Example 1:

Input:
```
board = [[-1,-1,-1,-1,-1,-1],
         [-1,-1,-1,-1,-1,-1],
         [-1,-1,-1,-1,-1,-1],
         [-1,35,-1,-1,13,-1],
         [-1,-1,-1,-1,-1,-1],
         [-1,15,-1,-1,-1,-1]]
```
Output:
```
4
```
Explanation: 
In the beginning, you start at square 1 (at row 5, column 0).
You decide to move to square 2 and must take the ladder to square 15.
You then decide to move to square 17 and must take the snake to square 13.
You then decide to move to square 14 and must take the ladder to square 35.
You then decide to move to square 36, ending the game.
This is the lowest possible number of moves to reach the last square, so return 4.

### Example 2:

Input:
```
board = [[-1,-1],[-1,3]]
```
Output:
```
1
```

## Constraints

- `n == board.length == board[i].length`
- `2 <= n <= 20`
- `board[i][j]` is either -1 or in the range `[1, n^2]`.
- The squares labeled 1 and `n^2` do not have any ladders or snakes.


                                         import java.util.*;

                                          class Solution {
                                          public int snakesAndLadders(int[][] board) {
                                          int n = board.length;
                                          int target = n * n;

                                          Queue<Integer> queue = new LinkedList<>();
                                           queue.offer(1);
                                           boolean[] visited = new boolean[target + 1];
                                           visited[1] = true;

                                          int moves = 0;

                                          while (!queue.isEmpty()) {
                                          int size = queue.size();
                                           for (int i = 0; i < size; i++) {
                                            int current = queue.poll();

                                                if (current == target) {
                                                    return moves;
                                                 }

                                                           for (int next = current + 1; next <= Math.min(current + 6, target); next++) {
                                                          int[] coordinates = getCoordinates(next, n);
                                                              int row = coordinates[0];
                                                              int col = coordinates[1];

                                                               int dest = board[row][col] == -1 ? next : board[row][col];
                    
                                                              if (!visited[dest]) {
                                                                      visited[dest] = true;
                                                              queue.offer(dest);
                                                            }
                                                         }
                                                      }
                                                          moves++;
                                                 }

                                                          return -1;
                                                  }

                                                 private int[] getCoordinates(int num, int n) {
                                                   int row = (num - 1) / n;
                                                    int col = (num - 1) % n;

                                                     if (row % 2 == 1) {
                                                    col = n - 1 - col;
                                                        }

                                                    row = n - 1 - row;

                                              return new int[]{row, col};
                                                 }
                                             }


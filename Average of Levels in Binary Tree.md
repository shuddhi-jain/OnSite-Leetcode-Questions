# Average of Levels in Binary Tree

## Problem Description

Given the root of a binary tree, return the average value of the nodes on each level in the form of an array. Answers within 10^-5 of the actual answer will be accepted.

### Example 1:

Input:
[3,9,20,null,null,15,7]
Output:
[3.00000,14.50000,11.00000]
Explanation:
The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11.
Hence return [3, 14.5, 11].

### Example 2:

Input:
[3,9,20,15,7]
Output:
[3.00000,14.50000,11.00000]

## Constraints

- The number of nodes in the tree is in the range [1, 10^4].
- -2^31 <= Node.val <= 2^31 - 1

## Approach

We can solve this problem using Breadth-First Search (BFS) to traverse the tree level by level. While traversing each level, we can calculate the average value of the nodes on that level and store it in an array. Finally, we return the array containing the average values for each level.

## Implementation

Check the provided source code file for the Java implementation of the solution.

             /**
          * Definition for a binary tree node.
         * public class TreeNode {
         *     int val;
         *     TreeNode left;
         *     TreeNode right;
         *     TreeNode() {}
         *     TreeNode(int val) { this.val = val; }
         *     TreeNode(int val, TreeNode left, TreeNode right) {
         *         this.val = val;
         *         this.left = left;
         *         this.right = right;
         *     }
         * }
         */
       class Solution {
           public List<Double> averageOfLevels(TreeNode root) {
        List<Double> averages = new ArrayList<>();
        if(root == null)
            return averages;
         Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
         while(!queue.isEmpty()){
             long levelSum = 0;
             int count = queue.size();
             
             for(int i=0; i< count; i++)
             {
                 TreeNode node = queue.poll();
                 levelSum+=node.val;
                 
                 if(node.left!=null)
                     queue.offer(node.left);
                 if(node.right!=null)
                     queue.offer(node.right);
             }
             double average =(double)levelSum/count;
             averages.add(average);
         }
        return averages;
    }
    }

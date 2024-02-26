# Mirror Tree

## Problem Description

Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

### Example 1:

Input:
[1,2,2,3,4,4,3]
Output:
true
Explanation:
The binary tree is symmetric around its center.

### Example 2:

Input:
[1,2,2,null,3,null,3]
Output:
false
Explanation:
The binary tree is not symmetric.

## Constraints

- The number of nodes in the tree is in the range [1, 1000].
- -100 <= Node.val <= 100

## Approach

We can solve this problem using both recursive and iterative approaches. 
- In the recursive approach, we traverse the tree in a symmetric manner, comparing each pair of nodes along the way.
- In the iterative approach, we use a queue to perform a level-order traversal, checking whether each level of the tree is symmetric.

## Implementation

Check the provided source code file for both the recursive and iterative implementations of the solution

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
                               public boolean isSymmetric(TreeNode root) {
                                if(root==null)
                                    return true;
                                   return isSymmetric(root.left,root.right);
                                   }
                                    private boolean isSymmetric(TreeNode left, TreeNode right){
                                   if(left==null&&right==null)
                                       return true;
                                     if(left==null||right==null||left.val!=right.val)
                                          return false;
                                      return isSymmetric(left.left,right.right)&& isSymmetric(left.right,right.left);
                                     }
                                 }

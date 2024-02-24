# K-Similar Strings

## Problem Description

Given two strings s1 and s2, they are k-similar if we can swap the positions of two letters in s1 exactly k times so that the resulting string equals s2.

You need to find the smallest k for which s1 and s2 are k-similar.

### Example 1:

Input:
s1 = "ab", s2 = "ba"
Output:
1
Explanation:
The two strings are 1-similar because we can use one swap to change s1 to s2: "ab" → "ba".

### Example 2:
Input:
s1 = "abc", s2 = "bca"
Output:
2
Explanation:
The two strings are 2-similar because we can use two swaps to change s1 to s2: "abc" → "bac" → "bca".

## Constraints
- 1 <= s1.length <= 20
- s2.length == s1.length
- s1 and s2 contain only lowercase letters from the set {'a', 'b', 'c', 'd', 'e', 'f'}.
- s2 is an anagram of s1.

## Approach

We can solve this problem using Breadth-First Search (BFS) to explore all possible swaps and find the minimum number of swaps required to make the strings k-similar.

## Implementation

Check the provided source code file for the Java implementation of the solution.

      class Solution {
         public int kSimilarity(String s1, String s2) {
         if (s1.equals(s2)) return 0;

        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();

        queue.offer(s1);
        visited.add(s1);

        int swaps = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String curr = queue.poll();
                if (curr.equals(s2)) return swaps;

                int j = 0;
                while (curr.charAt(j) == s2.charAt(j)) j++;

                for (int k = j + 1; k < s1.length(); k++) {
                    if (curr.charAt(k) == s2.charAt(k) || curr.charAt(k) != s2.charAt(j)) continue;

                    String next = swap(curr, j, k);
                    if (!visited.contains(next)) {
                        queue.offer(next);
                        visited.add(next);
                    }
                }
            }
            swaps++;
        }

        return -1; // Should not reach here
    }

    private String swap(String str, int i, int j) {
        char[] chars = str.toCharArray();
        char temp = chars[i];
        chars[i] = chars[j];
        chars[j] = temp;
        return new String(chars);
    }
    }


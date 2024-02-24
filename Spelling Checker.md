# Spelling Checker

## Problem Description

Given a wordlist, we want to implement a spell checker that converts a query word into a correct word.

For a given query word, the spell checker handles two categories of spelling mistakes:

1. **Capitalization**: If the query matches a word in the wordlist (case-insensitive), then the query word is returned with the same case as the case in the wordlist.
   
   Examples:
   - wordlist = ["yellow"], query = "YellOw": correct = "yellow"
   - wordlist = ["Yellow"], query = "yellow": correct = "Yellow"
   - wordlist = ["yellow"], query = "yellow": correct = "yellow"

2. **Vowel Errors**: If after replacing the vowels ('a', 'e', 'i', 'o', 'u') of the query word with any vowel individually, it matches a word in the wordlist (case-insensitive), then the query word is returned with the same case as the match in the wordlist.
   
   Examples:
   - wordlist = ["YellOw"], query = "yollow": correct = "YellOw"
   - wordlist = ["YellOw"], query = "yeellow": correct = "" (no match)
   - wordlist = ["YellOw"], query = "yllw": correct = "" (no match)

The spell checker operates under the following precedence rules:

- When the query exactly matches a word in the wordlist (case-sensitive), return the same word back.
- When the query matches a word up to capitalization, return the first such match in the wordlist.
- When the query matches a word up to vowel errors, return the first such match in the wordlist.
- If the query has no matches in the wordlist, return the empty string.

Given some queries, return a list of words answer, where answer[i] is the correct word for query = queries[i].

### Example 1:

Input:
wordlist = ["KiTe","kite","hare","Hare"]
queries = ["kite","Kite","KiTe","Hare","HARE","Hear","hear","keti","keet","keto"]
Output:
["kite","KiTe","KiTe","Hare","hare","","","KiTe","","KiTe"]


### Example 2:

Input:
wordlist = ["yellow"]
queries = ["YellOw"]
Output:
["yellow"]

## Constraints

- 1 <= wordlist.length, queries.length <= 5000
- 1 <= wordlist[i].length, queries[i].length <= 7
- wordlist[i] and queries[i] consist only of English letters.

## Approach

We can solve this problem using various data structures like hash maps and sets to efficiently perform spell checking based on the provided rules. The solution can be implemented in a way that efficiently handles different cases of spelling mistakes while maintaining the required precedence rules.

## Implementation

Check the provided source code file for the Java implementation of the solution.

      class Solution {
         public String[] spellchecker(String[] wordlist, String[] queries) {
        HashSet<String> wordSet = new HashSet<>();
        HashMap<String, String> casemap = new HashMap<>();
        HashMap<String, String> vowel = new HashMap<>();
        
        for(String word : wordlist){
            wordSet.add(word);
            String lowerCase = word.toLowerCase();
            if(!casemap.containsKey(lowerCase)){
                casemap.put(lowerCase, word);
            }
            String vowelKey = replaceVowels(lowerCase);
            if(!vowel.containsKey(vowelKey)){
                vowel.put(vowelKey, word);
            }
        }
        String[] result = new String[queries.length];
        for(int i=0; i< queries.length; i++){
            String query = queries[i];
            if(wordSet.contains(query)){
                result[i] = query;
            }
            else
            {
                String lowerCaseQuery = query.toLowerCase();
                if(casemap.containsKey(lowerCaseQuery)){
                    result[i] =  casemap.get(lowerCaseQuery);}
                else
                {
                    String vowelQuery = replaceVowels(lowerCaseQuery);
                    result[i] = vowel.containsKey(vowelQuery) ? vowel.get(vowelQuery):"";
                }
            }
        }
        return result;
    }
    private String replaceVowels(String word){
        return word.replaceAll("[aeiou]", "_");
    }
    }

Leetcode experiences:
From 212: https://leetcode.com/problems/word-search-ii/
1. note that sometimes we do not need to instantiate a stack and a visit[][] to track the visit information, simply to change the data on the original board can significantly reduce the time and space complexity, as long as we remember to put the original value back once we had done the search 
2. to build a trie, we shall also record whether it is the final char of the string and store it into data
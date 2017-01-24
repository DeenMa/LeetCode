Leetcode experiences:
From 212: https://leetcode.com/problems/word-search-ii/
1. note that sometimes we do not need to instantiate a stack and a visit[][] to track the visit information, simply to change the data on the original board can significantly reduce the time and space complexity, as long as we remember to put the original value back once we had done the search 
2. to build a trie, we shall also record whether it is the final char of the string and store it into data

From 358: https://leetcode.com/problems/rearrange-string-k-distance-apart/
When we need a queue to apart the same char for k distance, the capacity for the queue is actually k - 1, not k.
for example if k = 3, then a string "abcabc"
when the queue already have "ab" and we cannot add an "a" since it is already inside, but we can add a "c" therefore the queue is "bc", instead of "abc".
next time if we add an "a", if the queue has "bc", then "a" can be added to the final string, and the queue will be updated to "ca". (if the queue has "abc" then "a" cannot be added, which violate the problem description)
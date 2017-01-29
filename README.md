Leetcode experiences:
From 212: https://leetcode.com/problems/word-search-ii/
1. note that sometimes we do not need to instantiate a stack and a visit[][] to track the visit information, simply to change the data on the original board can significantly reduce the time and space complexity, as long as we remember to put the original value back once we had done the search 
2. to build a trie, we shall also record whether it is the final char of the string and store it into data

From 358: https://leetcode.com/problems/rearrange-string-k-distance-apart/
When we need a queue to apart the same char for k distance, the capacity for the queue is actually k - 1, not k.
for example if k = 3, then a string "abcabc"
when the queue already have "ab" and we cannot add an "a" since it is already inside, but we can add a "c" therefore the queue is "bc", instead of "abc".
next time if we add an "a", if the queue has "bc", then "a" can be added to the final string, and the queue will be updated to "ca". (if the queue has "abc" then "a" cannot be added, which violate the problem description)

From 409: https://leetcode.com/problems/longest-palindrome/
for those characters with odd occurances, we need to take its even part, instead of not taking at all

From 146: https://leetcode.com/problems/lru-cache/
note that we can make head and tail dummy, especially when both of them are frequently changing, such as LRU cache
dummyhead is used when head is always changing, if we need tail information but tail is always updating, we can also consider to create a dummy tail

From 460: https://leetcode.com/problems/lfu-cache/
note that if we create two classes FNode and KNode and both of them extends Node, we need to cast when we are retrieving the data from super class. See example below:
class Node {
  Node prev;
  Node next;
}

class FNode extends Node {
  int f;
}

class KNode extends Node {
  int k;
}

FNode curF = nxtF.prev; // error: nxtF.prev is a Node, not a FNode
FNode curF = (FNode) nxtF.prev; // ok

From ?: we cannot store a 2-d point into hashset / map, instead, we can make this point 1d and then store. in this way we can search in the future
HashSet<Pair> set = new HashSet<>();
set.add(new Pair(1,2));
boolean b = set.contains(new Pair(1,2)); // this will return false since this Pair(1,2) has a difference address to the Pair(1,2) added to hashset


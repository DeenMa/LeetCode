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

From 166: https://leetcode.com/problems/fraction-to-recurring-decimal/
Note that for this problem (and for many other problems, think about it!), even if we are dealing with integers, we may also need to convert the intergers to long.
Reason: say we want to get Integer.MAX_VALUE - 1 / Integer.MAX_VALUE work, outputting decimals instead of a simple 0, we need to expand the numerator and denominator to long and numerator * 10 to get correct decimals.

From ?: 
String is not a primitive java type, but that does not mean that system will assign a space for String - it does not. Everytime there is a new assignment, it will be assigned to a new reference / space which is a copy to String
  String s0 = "0";
  String s1 = s0;
  s1 = "1";
  System.out.println(s0); // "0", keep unchanged

From 56: https://leetcode.com/problems/merge-intervals/
note that when we are doing Merge Intervals, or Skyscraper problem which involves the start and end of a matrix, we may consider to break the matrix into line segments consisting (index, info) which info == 1 is the start of the matrix and info == -1 means the end of the matrix. this will somewhat solve some problems.

From 382: https://leetcode.com/problems/linked-list-random-node/
algorithm of reservior sampling of s[n] - get a random value from n values
1. define a size k array (k is small enough) - r[k]
2. for i = 0 : n - 1 (while not end)
if (i < k) r[k] = s[i]
else:
    generate a random j = value from 0 : i
    if (int)j < k:
        r[j] = s[i];
finally get a random one from r[0 : k]

From 402: https://leetcode.com/problems/remove-k-digits/
to remove k digits to get the minimum value, is equivalent to remove all the descending sequences (keep the ascending sequence as much as possible). in this case, using a stack is a great choice, since we can use a stack and store the ascending numbers inside (whenever there is a number smaller than peek, simply pop the peek until empty or found the peek less or equal to current one)
## Notes for leetcode

#### starting at Dec 7, 2016, by keping


## Data structrues and Algorithms
****
<a name="MonotonicQueue"></a>
MonotoicQueue: add(), void remove(), and max().  
Store Pair(val, skips between this and prev) in a deque.  
To find max(), the pairs stored should be in decreasing order, and the head is the max.  
To add(): removeLast() all larger elements, then addLast().  
To remove(): reduce first count by 1 till 0, then remove first.  
(An alternative implementation is to only store the indices in the deque.)



## Problems
****
LC239 Sliding Window Maximum
1. A segment tree, O(nlg(n)).
2. Custom Linked-PriorityQueue, store linked nodes in array. O(nlog(n)). Hard to code up.
3. [Monotonic Queue](#MonotonicQueue). 


LC388 Longest Absolute File Path

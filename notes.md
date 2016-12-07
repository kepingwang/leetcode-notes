## Notes for leetcode

#### by keping


## Data structrues
<a name="MonotonicQueue"></a>
**MonotoicQueue**: add(), void remove(), and max().  
Store Pairs(val, skips between this and prev) in a deque.  
To find max(), the pairs stored should be in decreasing order, and the head is the max.  
To add(): removeLast() all larger elements, then addLast().  
To remove(): reduce first skips by 1 till 0, then remove first.  
(An alternative implementation is to only store the indices in the deque.)


<a name="BinaryIndexedTree"></a>
**BinaryIndexedTree**: update(int i, int val) and sum(int i).  
Array implementation, starting from index 1.  
Parent value is sum of children's values.  
Not all original numbers are stored. Only store sums.  
i's parent is (i + (i & -i)). (1 -> 2, 2 -> 4, 3 -> 4, 4 -> 8, 5 -> 6, 6 -> 8)  
(i & -i) will find the rightmost set bit of i.
update(int i, int val): add delta from leaf (i+1) to root.  
sum(int i): sumVal(i+1); add val and sumVal(i - (i & -i)).  
(sum(7) = val(7) + val(6) + val(4))  
Can initialize at all 0, and then update each.


<a name="SegmentTree"></a>
**SegmentTree**: update(int i, int val), resultRange(int i, int j).  
Tree implementation.  
Node stores the left and right indices of the sum range it represents.  
initialization: build recursively.  
update: add delta from root to leaf.  
resultRange: break down (i, j) to merge result of avail ranges in tree.  
Can be applied to sum, min, max...

****
## Algorithms
todo...


****
## Problems
LC239 Sliding Window Maximum  
1. A segment tree, O(nlg(n)).  
2. Custom Linked-PriorityQueue, store linked nodes in array. O(nlog(n)). Hard to code up.  
3. [Monotonic Queue](#MonotonicQueue).  

LC388 Longest Absolute File Path  
Just use a stack for the parent path.

LC340 Longest Substring with At Most K Disctinct Characters  
Two pointers, with a map to keep track of frequencies.

LC308 Range Sum Query 2D - Mutable  
Immutable case: store prefix sum.  
Mutable 1d: [BIT](#BinaryIndexedTree) or [Segment Tree](#SegmentTree)  
Mutable 2d: 2D [BIT](#BinaryIndexedTree) or [Quad Tree](https://en.wikipedia.org/wiki/Quadtree)

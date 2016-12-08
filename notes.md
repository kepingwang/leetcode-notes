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

<a name="Trie"></a>
**Trie**:  
Each node has **26** (or 256, or ...) children. Boolean flag to mark hasWord.  
Optimize prefix string search.

<a name="UnionFind"></a>
**UnionFind**:  
int[] p, p[i] is the parent if i.  
Keep int[] size.  
find(i) finds the root if i.  
union(i, j), find roots, makes larger tree the parent.  

<a name="IntervalTree"></a>
**IntervalTree**:
Add and remove intervals dynamically. Find if a given interval overlaps with any existing one.  
Node stores ((low, high), maxHighVal at this subtree) 
Nodes are ordered by low.  
If a node stores ((10, 15), 30), then its left subtree 
To search I: 
```
if hit, return true;
if (curr.left != null && curr.left.max > I.lo):
    go left; (or I won't over lap with left subtree)
else:
    go right;
```
If we go left and there is no hit. In left subtree there must be an interval [a, max], since `max > I.lo` and there is no overlapping, we know `I.hi < a`. Since the nodes are ordered by low, then there won't be overlapping either in right subtree.


****
## Algorithms

<a name="SweepLine"></a>
**Sweep Line**:  
Store left and right ends of line segments together, and sort these critical points.  
Do certain things on meeting left or right end point.
Usually keep a set of existing elements. (tree set for order)

Check out [**Geometric Search**](https://github.com/kepingwang/leetcode-notes/blob/master/slides/GeometricSearchPrinceton.pdf)!  
Rectangle Intersection Search = Sweep Line + Interval Tree.

<a name="TopologicalSort"></a>
**Topological Sort**:
1. DFS, push vertex value to stack after all subtrees. For each unvisited node, start dfs.  
Cycle Detection: white node (0) unvisited, grey node (1) visited but unfinished, black node (2) finished. There is cycle is a child is grey (meaning it's an ancestor).  
2. BFS (Kahn's algorithm), first insert all start nodes (outdegree == 0) into queue.
```
for each node m with an edge e from n to m do
    remove edge e from the graph
    if m has no other incoming edges then
        insert m into S
```


****
## Problems


LC388 Longest Absolute File Path  
Just use a stack for the parent path.

LC340 Longest Substring with At Most K Disctinct Characters  
Two pointers, with a map to keep track of frequencies.

LC308 Range Sum Query 2D - Mutable  
Immutable case: store prefix sum.  
Mutable 1d: [BIT](#BinaryIndexedTree) or [Segment Tree](#SegmentTree)  
Mutable 2d: 2D [BIT](#BinaryIndexedTree) or [Quad Tree](https://en.wikipedia.org/wiki/Quadtree)

LC425 Word Square  
```
b a l l  
a r e a  
l e a d  
l a d y  
```
Given words, find all possible word squares.  
DFS (or BFS) + [Trie](#Trie) for faster searching.

Google Phone 1: Find all identical subtrees in a binary tree  
Although it's a tree, hashing is the best way to find same.  
Calculate and store the hashCode of each node. O(n) all hash values.  
Traverse the tree, keep a hash set of existing nodes (subtrees),  
and find duplicates along the way.

LC298 Binary Tree Longest Consecutive Sequence  
LC320 Abbreviation (word -> (w1rd, 1ord, w3, ...))  
Graph searching, usually dfs.
Sometimes we add the result for each recursion,  
sometimes only at recursion termination.
Sometimes there is only one starting point, 
sometimes we create new starting points all along the way.  

LC271 Encode and Decode Strings  
Serialize string array. Header for string lengths.  
LC297 Serialize and Deserialize Binary Tree  
Tree serialization, level-order (bfs) or pre-order (dfs).  
Just write down null (as "X").

LC317 Shortest Distance from All Buildings  
Just stupid BFS from all buildings. Only minor optimization can be done.  

LC200 Number of Islands
LC305 Number of Islands II  
0 1 1  
1 0 0  
0 0 1  
3 islands  
Immutable case can use DFS.
Mutable only [Union Find](#UnionFind).

LC289 Game of Life  
Cellular automaton. Cell lives or dies depends on number of neighbors.
Must update all cells simultaniesly. 
The trick for O(1) space is to use int to store udpated state and original state together.

LC259 3Sum Smaller  
2Sum, 3Sum, similar. Sort and use two pointers left and right.  
If to find sum certain value, hashing may be used.

LC411 Minimum Unique Word Abbreviation  
It's NP hard?  
Bit Manipulation + DFS.  

LC391 Perfect Rectangle
Count the number of corners, so smart!  
Odd number corners only possible at corners of the big rectangle  

LC399 Evaluate Division (given some know equations, find val of target equation)  
Graph search, dfs.  

LC218 The Skyline Problem (find contours of some skylines)  
[Sweep Line](#SweepLine).

LC56 Merge Intervals  
For intervals, often times we can succeed by sorting on one end.

LC295 Find Median from Data Stream  
My stupid method: build a custom tree with count for duplicates.  
Smart approach: use one min heap and one max heap.

LC329 Longest Increasing Path in a Matrix  
DFS, optimize with memoization.

LC380 Insert Delete GetRandom O(1)  
ArrayList with HashMap(val, index in array)  
To remove, swap the target with last, and remove last.

LC315 Count of Smaller Numbers After Self for Each Number  
1. A BST allowing for duplicates.
2. Mergesort counting jumps from right to left.

LC294 Flip Game II (flip ++ to --, lose if cannot flip anymore)
DFS + memoization.  
Lose win game: if for you win for any of the possible next steps, then I lose.

LC276 Paint Fence (n posts, k colors, no 3 adjacent same color)  
Google 2: Eat pills, half at a time, probability of getting full pill at n times.  
Two types subproblem recursion, with memoization. (Or DP).

LC253 Meeting Rooms II (find number of meeting rooms required)  
[[0, 30],[5, 10],[15, 20]]. ans 2.
sort by starting time, and keep a heap max of ending time.
Merge meetings if a new starting time is later than max end time, else add meeting to heap.
Finally the number of meetings in heap will be the meeting rooms required.

LC269 Alien Dictionary (Given a sorted list of words, return order of chars)  
chars(or int) as nodes, directed edges indicating relative orders.  
Finally return the order by a [topological sort](#TopologicalSort).

LC239 Sliding Window Maximum  
1. A segment tree, O(nlg(n)).  
2. Custom Linked-PriorityQueue, store linked nodes in array. O(nlog(n)). Hard to code up.  
3. [Monotonic Queue](#MonotonicQueue).  

L42 Trapping Rain Water  
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.  
![trap-rain-water](https://github.com/kepingwang/leetcode-notes/blob/master/images/LC42_rainwatertrap.png?raw=true)  
[Monotonic Queue](#MonotonicQueue)

LC318 Maximum Product of Word Lengths  
Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters.  
Only O(n^2) solution :( Can optimize with bit manipulation. int has 32 bits, but lower case only 26 chars. So it's common to use bit manipulation for chars.

LC212 Word Search II
```
Given words = ["oath","pea","eat","rain"] and board =
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
Return ["eat","oath"].
```
Backtracking + [Trie](#Trie).  

Backtracking: note that backtracking is different from dfs. DFS is to find a certain target vertex, while backtracking is to find a matching path. So we visit each node at most once in DFS (visited[i] = true). But in backtracking we may visit each node multiple times in different paths, so we have to remember to REMOVE NODE FROM PATH AT END OF EACH RECURSION, in particular, if we only keep boolean[] visited, we have to reset visited[i] = false.  
If we are doing backtracking on a 2D board, we can save the space of `boolean[][] visited` by changing the values in the board.

Trie: First store all words in the trie (in particular, remember the words at leaf nodes). Then start backtracking using the board with the trie starting from each board position. This is really smart. Normally we would backtrack to search for one matching path, but here since multiple matching pathes may share the same prefix, we can actually search for multiple paths simultaneously.


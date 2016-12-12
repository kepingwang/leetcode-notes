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
(Lowest Common Ancestor in Tree can be reduced to range minimum query, smallest depth between two nodes in euler tour.)

**Threaded Binary Tree (Morris Traversal)**: O(1) space traversal  
Make all right child pointers that would normally be NULL point to the inorder successor of the node (if it exists).  
In-order traversal: start from leftmost node, print, if `curr is thread node`, `go to in-order successor`, else `go to the leftmost child in right subtree`.  
To build:  
```
1. Initialize current as root 
2. While current is not NULL
   If current does not have left child
      a) Print current’s data
      b) Go to the right, i.e., current = current->right
   Else
      a) Make current as right child of the rightmost node in current's left subtree
      b) Go to this left child, i.e., current = current->left
```
[link](http://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)

<a name="Trie"></a>
**Trie**:  
Each node has **26** (or 256, or ...) children. Boolean flag to mark hasWord.  
Optimize prefix string search.  Build recursively. 

<a name="UnionFind"></a>
**UnionFind**:  
int[] p, p[i] is the parent if i.  
Keep int[] size.  
find(i) finds the root if i.  
union(i, j), find roots, makes larger tree the parent.  
Path Compression: make grand parent to be parent while finding root. `p[i] = p[p[i]]`

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


**[Linked Sparse Matrix](http://btechsmartclass.com/DS/U1_T14.html)**  
**LFU Cache (Similarly)**  


****
## Algorithms



**Moore’s Voting Algorithm:** find majority in O(n)  
[Link](http://www.geeksforgeeks.org/majority-element/).  
First roung find one element, which must be majority if there exists a majority.
Second round Check whether it is majority.  

### Sorting Algorithms:

Can you implement merge sort and quick sort?

**Heap Sort:** Can be done O(nlog(n)) totally in-place, but has poor locality, bad cache performance.

<a name="CountingSort"></a>
**Counting Sort**:  
Based on integer keys between a specific range. For example, if we have keys 2, 3, 5, then the range is [0, 5]. We count frequency of each number within range, and then the prefix sum of frequency is the number's position in the output array (After putting a number, we have to decrease that position by 1). While putting input to positions in output, iterate from the right end of input to ensure stableness.  
 O(n+k) time, O(n+k) space, where k is range of keys.  

**Radix Sort**:
Do counting sort digit by digit (or bit by bit, or char by char) from the least significant digit. Takes time O(d * (n+b)), where d is number of digits, b is base number.  

Problem: Sort n numbers in range from 0 to n^2 – 1 in linear time  
Radix sort. If b is base size, there would be log_b(n^2) rounds, with O(n+b) each round. If we choose b = n, then we can finish in O(2 * 2n).

**Bucket Sort**:
Uniformly distributed floating point numbers within a range. Create n buckets, put input to buckets, and sort each bucket (insertion sort).  
![Bucket Sort](https://github.com/kepingwang/leetcode-notes/blob/master/images/buckect-sort.png)

### Geometric Search:
<a name="SweepLine"></a>
**Sweep Line**:  
Store left and right ends of line segments together, and sort these critical points.  
Do certain things on meeting left or right end point.
Usually keep a set of existing elements. (tree set for order)

Check out [**Geometric Search**](https://github.com/kepingwang/leetcode-notes/blob/master/slides/GeometricSearchPrinceton.pdf)!  
Rectangle Intersection Search = Sweep Line + Interval Tree.

### Graph Algorithms:  
Check out [Princeton Algorithms](http://algs4.cs.princeton.edu/40graphs/)

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

**Relaxation**:
```
private void relax(DirectedEdge e) {
    int v = e.from(), w = e.to();
    if (distTo[w] > distTo[v] + e.weight()) {
        distTo[w] = distTo[v] + e.weight();
        edgeTo[w] = e;
    }
}

private void relax(EdgeWeightedDigraph G, int v) {
    for (DirectedEdge e : G.adj(v)) {
        int w = e.to();
        if (distTo[w] > distTo[v] + e.weight()) {
            distTo[w] = distTo[v] + e.weight();
            edgeTo[w] = e;
        }
    }
}
```

**Dijkstra's Shortest Path**:  
Dijkstra's algorithm initializing dist[s] to 0 and all other distTo[] entries to positive infinity. Then, it repeatedly relaxes and adds to the tree a non-tree vertex with the lowest (priority queue) distTo[] value, continuing until all vertices are on the tree or no non-tree vertex has a finite distTo[] value. (Non-negative weights, directed or undirected.) O(E + Vlog(V))

**Topological Sort for Single Source Shortest Path in DAG**: (Allowing negative weights)  
Initialize distTo[] and relax vertices in topological order. O(E + V)  
Can also solve **Longest Path in DAG** by initializing dist to NEGATIVE_INFINITY, and switching the sense of the inequality in relax().

**Bellman Ford Shortest Path**:
Initialize distTo[]. Then, considering the digraph's edges in any order, and relax all edges. Make V such passes. Always O(VE).
* Queue Based Implementation: The only edges that could lead to a change in distTo[] are those leaving a vertex whose distTo[] value changed in the previous pass. To keep track of such vertices, we use a FIFO queue.  
* Negative Cycle: There is a negative cycle reachable from the source if and only if the queue is nonempty after the Vth pass through all the edges. Moreover, the subgraph of edges in our edgeTo[] array must contain a negative cycle.  
* Arbitrage Detection: Application of Negatice cycle detection.  
* Why it works: It first calculates the shortest distances for the shortest paths which have at-most one edge in the path. Then, it calculates shortest paths with at-nost 2 edges, and so on. After the ith iteration of outer loop, the shortest paths with at most i edges are calculated.

**Floyd Warshall All Pairs Shortest Path**:  
Update distance matrix between vertices, checking an intermediate vertex for all pairs, for all vertices as interdemiate.
```
/* Add all vertices one by one to the set of intermediate
   vertices.
  ---> Before start of a iteration, we have shortest
       distances between all pairs of vertices such that
       the shortest distances consider only the vertices in
       set {0, 1, 2, .. k-1} as intermediate vertices.
  ----> After the end of a iteration, vertex no. k is added
        to the set of intermediate vertices and the set
        becomes {0, 1, 2, .. k} */
for (k = 0; k < V; k++)
{
    // Pick all vertices as source one by one
    for (i = 0; i < V; i++)
    {
        // Pick all vertices as destination for the
        // above picked source
        for (j = 0; j < V; j++)
        {
            // If vertex k is on the shortest path from
            // i to j, then update the value of dist[i][j]
            if (dist[i][k] + dist[k][j] < dist[i][j])
                dist[i][j] = dist[i][k] + dist[k][j];
        }
    }
}
 ```
 
**Minimum Spanning Tree**:  
* Cut Property: Given any cut in an edge-weighted graph (with all edge weights distinct), the crossing edge of minimum weight is in the MST of the graph.  
* Greedy Algorithm: Start with all edges gray, find a cut with no black edges, color its minimum-weight edge black. Loop until V-1 edges are colored black.  


**Prim's Algorithm MST**:  
Attach an edge to a single growing tree at each time.
![prim](https://github.com/kepingwang/leetcode-notes/blob/master/images/prim.png)  
* Lazy Implementation O(Elog(E)):  
![prim-lazy](https://github.com/kepingwang/leetcode-notes/blob/master/images/prim-lazy.png)
* Eager Implementation O(Elog(V)): maintain on the priority queue just one edge for each non-tree vertex: the shortest edge that connects it to the tree.  
![prim-eager](https://github.com/kepingwang/leetcode-notes/blob/master/images/prim-eager.png)

**Kruskal's Algorithm MST**:
Each time color black an minimum-weight gray edge that doesn't form a cycle with existing black edges.  
![kruskal](https://github.com/kepingwang/leetcode-notes/blob/master/images/kruskal.png)  
Implementation O(Elog(E)): priority queue to consider the edges in order by weight, _a **union-find** data structure to identify those that cause cycles_, and a queue to collect the MST edges.

### String Algorithms:

**KMP (Knuth Morris Pratt) Pattern Searching**:
Given a text txt[0..n-1] and a pattern pat[0..m-1], write a function search(char pat[], char txt[]) that prints all occurrences of pat[] in txt[]. You may assume that n > m. O(n)   
```
Input:  txt[] =  "AABAACAADAABAAABAA"
        pat[] =  "AABA"
Output: Pattern found at index 0
        Pattern found at index 9
        Pattern found at index 13
```
Bad case for naive algorithm:  
```
txt[] = "ABABABCABABABCABABABC"
pat[] = "ABABAC"
```
KMP basic idea: avoid matching chars that we already know will match. Uses degenerative property of the pattern (pattern having same sub-patterns appearing more than once).  
**Preprocessing**: Construct an aux array lps[]. lps[i] is the len of the longest prefix in s[0...i] that is also a suffis of s[0...i]. Then when we have a mismatch at j, we set j = lps[j-1];
See [geeksforgeeks](http://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/) for detailed explanation.


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

Trie: First store all words in the trie (in particular, remember the words at leaf nodes). Then start backtracking using the board with the trie starting from each board position. This is really smart. Normally we would backtrack to search for one matching path, but here since multiple matching paths may share the same prefix, we can actually search for multiple paths simultaneously.

LC421 Maximum XOR of Two Numbers in an Array O(n)  
Bit Manipulation and Trie. Not all trees are O(log(n)) search, Trie is O(M) search, where M is number of characters per word (or here number of bits in a num).

LC128 Longest Consecutive Sequence O(n)  
1. HashMap and [Union-Find](#UnionFind). O(nlog(n)) in theory.  
2. O(n) Solution: Store numbers in set, and check each streak from its start. A num is the start of a streak if (n-1) doesn't exist in set.  
3. Store the (num, streak len) in map, so that when inserting a num between, left and right ends of streak can be found by streak len, and thus can be updated.

LC274 H-Index: A scientist has index h if h of his/her N papers have at least h citations each, and the other N − h papers have no more than h citations each.  
1. Sorting is easy.  
2. [Counting Sort](#CountingSort)

LC162 Find Peak Element in Array. O(log(n)) required.  
For some very simple array search problem, try to find log(n) solution! Find local maximum, mid2 = mid1+1, compare `nums[mid1]` and `nums[mid2]`  

LC139 Word Break  
Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.  
For example, given  
s = "leetcode",  
dict = ["leet", "code"].  
Return true because "leetcode" can be segmented as "leet code".  
1. Dynamic Programming  
2. DFS + memoization, with Trie optimization.

LC52 Max-Sum Contiguous Subarray (Kadane's algorithm)  
DP focuses on the ending point, not the starting point. When start doesn't make sense, try end.  
```
public static int maxSubArray(int[] A) {
    int maxSoFar=A[0], maxEndingHere=A[0];
    for (int i=1;i<A.length;++i){
    	maxEndingHere= Math.max(maxEndingHere+A[i],A[i]);
    	maxSoFar=Math.max(maxSoFar, maxEndingHere);	
    }
    return maxSoFar;
}
```

LC375 Guess Number Higher or Lower II: guess(m) pay m, what's the minimum cost to guarantee success.  
Not Binary Search. But DP. For each number x in range[i~j]  
we do: result_when_pick_x = x + max{DP([i~x-1]), DP([x+1, j])}  
--> // the max means whenever you choose a number, the feedback is always bad and therefore leads you to a worse branch.
then we get DP([i~j]) = min{xi, ... ,xj}  
--> // this min makes sure that you are minimizing your cost.  

LC410 Split Array Largest Sum (Split into m subarrays, minimize max sum)  
Smart! It takes O(n) to find whether we can find m subarrays whose max sum <= a given target.  
So use this isValid(target) to do binary search (between maxNum and totalSum).  

LC356 Line Reflection  
First get mirror position, store all points in hash set. Then for each point, check whether its reflection is in set.  
Can use String to encode pair. set.add(p[0]+","+p[1]);  

LC240 Search a 2D Matrix II (rows ordered, cols ordered, find target)  
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
Really Smart! Start from top-right corner, compare current num with target,  
if `target < num`, target cannot be in this column;  
if `target > num`, target cannot be in this row.

LC5 Longest Palindrome:  
Extend palindrom from middle (odd, even). Best only O(N^2).  
LC214 Shortest Palindrome (add to front to make s palindrome):  
```
Given "aacecaaa", return "aaacecaaa".
```
1. Reduce to finding the longest Palindrome starting at 0.
2. So Smart! Reduce to finding the KMP lps[] for the string: "s+#+s.reverse()"  

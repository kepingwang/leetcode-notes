### Interview Problems for Google
 -- sources are online forums 
 
 
G1 Design a set with O(1) add(), remove(), getRandom()
 
G2 Char binary tree. Smallest str of leaf to root path.
 
G3 Given a set S of 10^6 doubles. Find [X, X+1) half-open real interval contains as many elements of S as possible.
 
G4 Light Bulb. Switch, every, every two, every three... bulbs. Find the value for a given bulb.
 
G5 Find number of target in sorted array. O(log(n)) instead of O(k + log(n)), where k is number of target.
 
G6 Find number of discontinous matches of first string in second one.  
Example: "cat", "catapult" -> [“CATapult”, “CatApulT”, “CAtapulT”] return number 3.  

G7 Find all identical (duplicate) subtrees in a binary tree  

G8 Tell whether a directed connected graph is a tree. (Tree node cannot have two parents!)  

G9 Eat pills, half at a time, probability of getting full pill at n times.  

G10 m factories, k colors of candies. A demand array for all kinds of candies.
A factory produce one candy at one period, can only produce one color candy. How fast can all demand be met.

G11 A stock price chart, how to smooth the fluctuation. What problem can occur?

G12 Given an array, first increasing, then decreaing［1，2，4，5，6，4，2]. Find the max.  

G13 ??? 两个二维矩阵，都是1和0组成，1代表房子的灯亮着，0代表房子的灯关了，矩阵1代表某一天某个位置观察这个社区的灯亮的情况，矩阵2代表过了一段时间后相同位置观察社区的灯亮情况，由于地球的自转，可能观察到灯亮的房子的位置发生的转移，转移方向由一个（x,y）代表，x为正代表向右移动x步，为负代表向左移动-x步，y类似的表示但是代表的是上下。需要注意的是，过了一段时间后，有些房子原来是关灯，现在又开了，所以矩阵1和矩阵2中1的数目可能不等。求最可能的（x,y）是什么。

G14 给一个二叉树，求出最长的valid path的长度，valid path的定义是：1.path中的元素都是相邻的递增或者递减的，如［1，2，3，4。。］或者［4，3，2，1。。］，2.path的构成可以是从child－parent－child也可以是不打折的path。 Follow－up：基于上题修改两个条件：1.这是一个一般的树，而不是二叉树；同时2.valid的序列不一定是相邻的，任意间隔的等差数列都可以。 

G15 给一个string A，如“abpppleles”,和一个string array，如["able", "pplle","fdse"...],求出array中是A的subsequence的最长的一个string，如果有多个，随便输出一个。 

G16 简化债务关系，就是给一堆人的账面交易记录，求最少交易次数使得账面平衡。

G17 返回一棵树里面所有的 爸爸->我->儿子 的序列

G18 Find the contiguous subarray whose sum equal to a certain value.

G19 Print all prime numbers smaller than n.


****
 
### Solutions (hints):
 
G4 A num has even number divisors, unless it's a square number.

G5 Binary Search, recurse two when `nums[mid]` is target

G6 Dynamic Programming.

G7 Although it's a tree, hashing is the best way to find same.  
Calculate and store the hashCode of each node. O(n) all hash values.  
Traverse the tree, keep a hash set of existing nodes (subtrees),  
and find duplicates along the way.

G8 Use HashSet!

G9 Two types subproblem recursion, with memoization. (Or DP).

G10 Greedisgood.

G11 LC346 given a window size,find moving average from data stream.  
Double calculation loses precision after many times. Need to recalculate from time to time.

G18 Use HashSet! First store all prefix sums. Then find (target-prefixSum) in set for each prefixSum.  
If the goal contains "number equals", then it often involves hash set. Hash Set can compare one 
element against many elements in O(1).

G19 Sieve of Eratosthenes. (Efficient when N is smaller than 10 million. O(n) space.)  
Eliminate multiples of 2, 3, 5, ... p <= sqrt() 




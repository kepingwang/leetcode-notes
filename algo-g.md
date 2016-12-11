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

G13 两个二维矩阵，都是1和0组成，1代表房子的灯亮着，0代表房子的灯关了，矩阵1代表某一天某个位置观察这个社区的灯亮的情况，矩阵2代表过了一段时间后相同位置观察社区的灯亮情况，由于地球的自转，可能观察到灯亮的房子的位置发生的转移，转移方向由一个（x,y）代表，x为正代表向右移动x步，为负代表向左移动-x步，y类似的表示但是代表的是上下。需要注意的是，过了一段时间后，有些房子原来是关灯，现在又开了，所以矩阵1和矩阵2中1的数目可能不等。求最可能的（x,y）是什么。

G14 给一个二叉树，求出最长的valid path的长度，valid path的定义是：1.path中的元素都是相邻的递增或者递减的，如［1，2，3，4。。］或者［4，3，2，1。。］，2.path的构成可以是从child－parent－child也可以是不打折的path。 Follow－up：基于上题修改两个条件：1.这是一个一般的树，而不是二叉树；同时2.valid的序列不一定是相邻的，任意间隔的等差数列都可以。 

G15 ??? 给一个string A，如“abpppleles”,和一个string array，如["able", "pplle","fdse"...],求出array中是A的subsequence的最长的一个string，如果有多个，随便输出一个。 

G16 简化债务关系，就是给一堆人的账面交易记录，求最少交易次数使得账面平衡。

G17 返回一棵树里面所有的 爸爸->我->儿子 的序列

G18 Find the contiguous subarray whose sum equal to a certain value.

G19 Print all prime numbers smaller than n.

G20 设计一个相当于家谱的class，实现3个函数  
void birth(string parentname, string childname)  
void death(string name)  
vector orderofsuccession()  
假设每个parent能够有无数个孩子，不考虑结婚的问题，每个孩子都只有一个parent。第三个函数就是按照顺序输出每一个还活着的人
Follow up:  
1）如果每个人有年龄，输出是同一代的人按照年龄排序   
2) 输出的顺序换成先输出年龄最大人，然后输出此人的所有孩子，再输出同一代比他年龄小的人  
3) * 如果这个家族人特别多，没法用queue来存储进行level order traverse怎么办.

G21 设计一个HistroricMap：HistroricMap hmap();  
hmap.insert("foo",1) at time 1;  
hmap.insert("foo", 2) at time 5;  
hmap.at("foo",3)=1; （第二个参数代表时间） 
hmap.at("foo",5)=2;  
说如何把存的复杂度变成O(1)，取的复杂度还是O(log T).

G22 ??? 给一个array， 一个window size, 你可以任意取任意数量的元素，要保证和最大，条件是任意两个元素的index之差必须大于等于给定的window size（感觉不应该叫window,应该叫step,就是这个地方搞得我一开始理解不了题意）， 且不能重复取同一个元素（index 相同）。如果一个元素都不取，和就是0。array中可以含有负数。

G23 选举投票，给一个list of votes, 每个vote里面包含name和timestamp，另一个输入是一个截止的timestamp，要输出在这个截止的timestamp之前，谁获得的票数最多。 Follow up是输出top k，用heap做的. 给了k个人de名字求何时这几个人领先。  

G24 在phone digital board上给你一个初始位置（0-9是valid的，左下，右下两个按键不考虑）和总共走的次数n，然后假设在初始位置上有一个国际象棋的knight，按照knight跳的规则（跟中国象棋的马的规则一样，马走日）跳n次，问你总共有多少种跳的可能性。(BFS, DFS or DP)  

G25 给一个string,一个整数k,把string 切成k份让每一份的首字母都不一样。只需返回一个结果。

G26 8 * 8国际象棋棋盘，给定Knight的起始和结束位置，输出最短的从起点到终点的路径。

G27 给个01二维矩阵，求所有为0的点到最近的1的距离，返回是个矩阵。

G28 问关于连续的序列这种。1题很简单，好像就sort一下，已经不记得题目了；2题求是否这个array可以组成恰好若干5个连续的序列 例如［1，2，2，3，3，4，4，5，5，6］就反悔true因为可以组成12345，23456，问了数字没有上线，可以认为是正的；3题求是否这个array可以组成恰好若干x个连续的序列,这里x要大雨3 例如［1，2，2，3，3，4，4］返回true 因为可以组成1234，234。

G29 ??? 给你好多点的坐标((0,1),(2,1),(4,1)(3,6)(7,9)(5,0)(0,6)(8,3))，问你这些点能组成的长方形中，面积最小是多少？

G30 ??? Given a word, find the minimum number of steps required to convert word to a word with SS pattern. (each operation is counted as 1 step.)e.g : cdcc -> cdcd 或者 ccc -> cc You have the following 3 operations permitted on a word:a) Insert a character b) Delete a character c) Replace a character

G31 Find if a given string can be represented from a substring by iterating the substring “n” times. [link](http://www.geeksforgeeks.org/find-given-string-can-represented-substring-iterating-substring-n-times/)  

****

### Solutions (hints):
 
G4 A num has even number divisors, unless it's a square number.

G5 Binary Search, recurse two when `nums[mid]` is target

G6 Dynamic Programming. LC115  

G7 Although it's a tree, hashing is the best way to find same.  
Calculate and store the hashCode of each node. O(n) all hash values.  
Traverse the tree, keep a hash set of existing nodes (subtrees),  
and find duplicates along the way.

G8 Use HashSet!

G9 Two types subproblem recursion, with memoization. (Or DP).

G10 Greedisgood.

G11 LC346 given a window size,find moving average from data stream.  
Double calculation loses precision after many times. Need to recalculate from time to time.

G13 用hashmap存矩阵2中1的位置，iterate所有可能的转移(x,y)，然后计算转移后的位置，看有多少位置在hashmap中，记录位置最多的那个转移(x,y)，对了，题目给出，矩阵中1的数目远小于矩阵的边长，所以注意转移(x,y)的可能性只需要矩阵1和2中的1的点，如矩阵1中有a个1，矩阵2中有b个1，那可能的(x,y)最多ab个。

G15 ?? 考虑结合hashmap和binary search，用一个prev纪录过去的index，每次BS搜当前hash map中char对应的indexs list中大于prev的第一个的。

G18 Use HashSet! First store all prefix sums. Then find (target-prefixSum) in set for each prefixSum.  
If the goal contains "number equals", then it often involves hash set. Hash Set can compare one 
element against many elements in O(1).

G19 Sieve of Eratosthenes. (Efficient when N is smaller than 10 million. O(n) space.)  
Eliminate multiples of 2, 3, 5, ... p <= sqrt() 

G20 Follow up (3): LC116. Link nodes in each level.

G21 Just put time to hashMap, since time is increasing. Then fetch and do binary search.

G23 Find top k elements.  
1. Use a heap. O(nlog(k))  
2. Quick Select. O(n^2) worst case, O(n) on average.
3. Median-of-medians (BFPRT). Guarantee O(n), but large constant.

G25 Save chars and their pos to array, and sort.

G26 BFS. Just has to store parent as pair (x, y).

G27 Can BFS from each 0, but a better idea is to use flooding from 1.  
(Somewhat like finding prime numbers, sometimes the best why is not to find the desired, but to eliminate the undesired.)

leetcode 310. Minimum Height Trees
题目大意是以哪些结点为根结点构建出来的树的高度最小，找出最靠近中心的结点，
好比是剥洋葱，一层层去除，入度为1的即为叶子结点，剥离，上一层有的可能也变成叶子结点，这样就等同于拓扑排序，可以用广度优先BFS
另外一种思路是找到两个结点之间的最长距离然后取中点，即为所求


怎么去除？在哪里停？
用map记录关联关系，遍历删除的时候要小心存在mapconcurrent异常
相对的解决办法是用list记录关联关系，以index作为结点
参考链接：
https://www.cnblogs.com/yrbbest/p/5060225.html
https://www.jianshu.com/p/21a1af84b0f9

三种思路解题
https://blog.csdn.net/Yaokai_AssultMaster/article/details/52051181

首先随便取一个点，找到和它距离最远的点，然后从最远的点出发找最远的点
具体做法：通过两次BFS或者DFS找到最大长度路径，然后取中点,偶数个点则为中间两点

332. Reconstruct Itinerary
飞机票行程，走遍所有的地点，如果多种方案则按字母顺序小的，心中有一个模糊的方案是map，但是怎么走遍所有的点呢，
参考方案是DFS，其中map的value是priorityqueue可以保证顺序，同时不重复，弹出管理队列
refer: https://www.cnblogs.com/Dylan-Java-NYC/p/5309418.html

399. Evaluate Division
思路类似但是写的混乱，排除已走过的结点没有处理好，还有对应值，可以通过两个map加上list的形式对应起来
refer: https://www.cnblogs.com/271934Liao/p/7263162.html

*684. Redundant Connection
无向图中环的检测
其实和选课的题一样，不过检测流程改一下，边添加边检测到底是哪个边，而不是全部加完，哪个边都可以是构成环的边，DFS，BFS均可
另外一种解法参考union find
https://www.cnblogs.com/grandyang/p/7628977.html

**685. Redundant Connection II
leetcode B站有视频


743. Network Delay Time
网络延迟时间，取决于它的路径中耗时最长的，可以广度优先，统计所有点的耗时
刚开始想的挺简单，遍历一遍比较即可，但是考虑到路径选择，还有不能到达的点就乱了，不知如何下手，因为广度优先在路径有权重的情况下是不合适的，

有权图求最短路径用迪克斯特拉算法
https://blog.csdn.net/afei__/article/details/83780362


785. Is Graph Bipartite
题目意思没读懂，看了博客才明白，二维数组中的每个元素数组代表这个点的邻接点，根据给的数组信息判断图能不能二等分，无交集，
参考解法是染色法，具体又可以分为DFS，BFS；在DFS中检查每一个路径，递归调用，每个结点有三个值，0，初始状态，没有检查过，1或者-1表示已经检查染色，
如果没有检查过就递归调用检查染色，如果检查过了，则判断相邻顶点的颜色是否和当前顶点相反，相反则继续检查下一个顶点，相同则终止，说明不能二等分。
BFS有个难点是要找到中心，才能一层层的扩散开来，解决方案是遍历所有顶点,假设每一个都是中心，标记之，同时对未染色的邻顶点标记为相反颜色，已染色的也是检查颜色是否相反。  

*765. Couples Holding Hands
两两组对问题，要两个相邻的数在一起，贪心算法看懂了，不符合要求的直接变，
union find连通算法则是假设两两一组，全部需要交换，约定/2为根结点，也是两两取出来，
如果它们的根结点相同，那组数就减一，因为可以合并，最后交换值就是减少的组数


802. Find Eventual Safe States
有向图中能到达出度为0的点都算，一个方法是找这些点，从最开始出度为0的点开始倒推，和这些点连接且出度为1的也是安全的，那么需要一个数组来记录每个点的出度
另外一个是找不组成环的路径上的点直接用DFS


839. Similar String Groups
一个数组字符串，如果一个字符串中交换两个字符的位置和另外一个字符串相等，就判定它们相似，问这样的字符串有多少组，
一个方法是用union find的思想，把所有相似的字符串的根结点设置为同一个，那么它们就相似了
另外一个方法是DFS，遍历数组，把遍历的每个字符串找到所有和它相似的递归查找，加入已经归组的set中，只要是新出现的就算新的一组
refer：https://buptwc.com/2018/06/05/Leetcode-839-Similar-String-Groups/
https://www.cnblogs.com/grandyang/p/11503433.html

841. Keys and Rooms
能否走完所有房间，想法是深度遍历或者广度遍历，有一个set记录走过的房间，数量少于房间数则不能走遍所有房间，？
广度遍历犯了一个错误，0的相邻点没有加入set 
深度遍历则是从0出发判断能不能到达其他房间
也可以说检查除0之外有入度为零的房间也就是不能到达的房间，这只是一种情况，还有别的情况是形成了几个环的怎么判断？

**854. K-Similar Strings 
开始想的简单，觉得和839题有点像，交换位置之后单词相同，那找到不同数目除2就可以了，但是像abc,cab这种情况就不好弄了，
refer： https://www.cnblogs.com/grandyang/p/11343552.html

**928. Minimize Malware Spread II
题目没看懂


5. Longest Palindromic Substring
笨办法就是遍历组合判断
优化方案一：
根据对称的两种方式，以对称位置向两边扩散
马拉车算法没看懂

6. ZigZag Conversion
最直接的想法是按照二维数组的赋值规律来，2*rowNums-2为步长，根据每个值对应的坐标来一一赋值
目前没有看到更好的办法

10. Regular Expression Matching
情况很多，考虑不周到,重点考虑*的情况0或者很多个，递归调用或者动态规划
https://www.cnblogs.com/grandyang/p/4461713.html


8. String to Integer (atoi)
以为是很简单的题，字符串中提取带符号的数字，结果写的乱七八糟，很多地方考虑不周到，比如停止条件，数字超过边界的判断
优化方案是用当前sum值判断是否可能越界，符号在最开始判断，不在循环中，通过越过空格，标记循环起始位置，而非每次都去截取重新获得字符串的值
refer：
https://www.cnblogs.com/grandyang/p/4125537.html


17. Letter Combinations of a Phone Number
很简单的题，map列出对应关系，组合遍历即可


22. Generate Parentheses
从简单的开始，发现排列组合的规律，
n=1:
()

n=2,在n=1的基础上插入一组括号，位置如下：
在0的位置  ()()
在1的位置  (())

n=3,在n=2的基础上插入一组括号，遍历n=2的括号组合：
当n=2，在第0个组合的基础上，即在括号为()()的基础上插入一组括号，位置如下：
在0的位置 ()()()
在1的位置 (())()
在2的位置 ()()()
在3的位置 ()(())

当n=2，在第1个组合的基础上，即在括号为(())的基础上插入一组括号，位置如下：
在0的位置 ()(())
在1的位置 (()())
在2的位置 ((()))
在3的位置 (()())

......

以此类推，可以看到组合会有重复的情况，需要过滤判断

还有一种递归求解的方法,分别添加左括号右括号，并控制它们的数量
refer:
https://www.cnblogs.com/grandyang/p/4444160.html

*38. Count and Say
没看懂题目
https://zhuanlan.zhihu.com/p/34300515

30. Substring with Concatenation of All Words
简单粗暴的方法就是遍历截取出字符串数组的所有字符串的长度，再均匀分割，和字符串的map做对比看是否全部包含

32. Longest Valid Parentheses
stack计数是个问题,想不清楚,
解决方案：根据stack记录的位置以及开始计数的位置可以算出当前有效括号的数量
第二种方法是动态规划，状态转移方程没看懂
第三种是记录左右括号的数量，如果左右括号数量相等，那肯定是有效的，不相等时则计数清零，防止特殊情况下，则可以顺序、逆序分别计数
refer:
https://www.cnblogs.com/grandyang/p/4424731.html


43. Multiply Strings
模拟多位数相乘的过程，错位相加
referer:
https://www.cnblogs.com/grandyang/p/4395356.html

*44. Wildcard Matching
递归调用，写的很啰嗦，还是超时了，需要剪枝优化

一种巧妙的方法是，记录p中星号的位置，匹配更新，
另外一种是动态规划
refer：
https://www.cnblogs.com/grandyang/p/4401196.html

*65. Valid Number
需要考虑的情况太多了！！
一个月之后，2020/1/7又跪了

*68. Text Justification
拆分法，先确定每一行是哪几个单词，再看看这几个单词怎么填充，卡在填充这里了，没看到特别好的方法

72. Edit Distance
用动态规划还是挺简单的，只考虑状态转移方程式，从一个状态变成另外一个状态的情况
还有一种解法是递归计算，不相等的情况下三种操作插入、删除、替换三种方式分别计算次数
refer:
https://www.cnblogs.com/grandyang/p/4344107.html

91. Decode Ways
思路上是往动态规划靠拢，没想清楚状态转移方程
refer：
https://www.cnblogs.com/grandyang/p/4313384.html


*93. Restore IP Addresses
没有思路
一是只要遇到字符串的子序列或配准问题首先考虑动态规划DP，二是只要遇到需要求出所有可能情况首先考虑用递归。


788. Rotated Digits
题意理解偏差


791. Custom Sort String
比较简单，queue记录顺序，map记录次数，也可以用数组的形式


415. Add Strings
简单题，目前没找到更好的方法

434. Number of Segments in a String
简单，不值一提，直接spilt分割即可

443. String Compression
简单，双指针，一个记录当前遍历到哪个字符串，一个记录次数


459. Repeated Substring Pattern
简单题，按步长切割，步长最长为字符串长度的一半，如果长度不是步长的整数倍直接跳过，否则切割验证每个部分的值是否一致

468. Validate IP Address
简单题，就根据ip的特点分段判断

520. Detect Capital
简单题，根据单词的规范分情况讨论


*521. Longest Uncommon Subsequence I
没看懂题目意思
看了解析，确实是简单题。。。一行搞定了，吐血。。。
refer：
https://www.cnblogs.com/grandyang/p/6666839.html

*522. Longest Uncommon Subsequence II
521的衍生，暴力破解
https://github.com/mufanlee/LeetCode/blob/master/522.Longest-Uncommon-Subsequence-II.md

537. Complex Number Multiplication
简单题，根据复数乘法的规则来实现，合并乘积即可

539. Minimum Time Difference
暴力破解超时，用优先级队列排序了，避免很多无用计算，因为最小值绝对在两个相邻的时间点之间，特殊情况是最小的时间和最大的时间，再单独计算一下
一个是时分分开的按字符串排序，一个是换算成分钟排序，时间都是nlogn
还有一种时间复杂度为n的方法，因为一天的分钟数量有限，所有可以以长度为1440的整形数组计数，如果出现值为1，如果出现2次那肯定是最小的时间差0，如果每个都出现一次，那么从index为0开始遍历，天然就是从小到大的顺序
refer:
https://www.cnblogs.com/grandyang/p/6568398.html

541. Reverse String II
简单题，根据题目要求翻转即可，以k为步长，index记录当前分组数，判断是否翻转
更简洁的方法，直接以2k为步长，遇到就翻转，省去index计数
refer:
https://www.cnblogs.com/grandyang/p/6583004.html


53. Maximum Subarray
简单的动态规划，想清楚dp[i]的含义，在这里是以nums[i]为最后一个元素的子序列，
那么dp[i]和dp[i-1]的关系就出来了，有三种情况
第一种情况是dp[i-1]是负数,dp[i-2]也是负数，nums[i]>=0>dp[i-1],那么重新开始一个子序列，以nums[i]为第一个元素,即dp[i]=nums[i]
第二种情况是dp[i-1]是正数,dp[i-2]是负数，那么nums[i]接上前面的子序列，即dp[i]=dp[i-1]+nums[i];
第三种情况是dp[i-2]是正数,dp[i-1]是负数，，那么dp[i-1]小于dp[i-2],即dp[i]=dp[i-2]+nums[i-1]+nums[i];

62. Unique Paths
简单题，动态规划最关键的就是相邻状态之间的关系，
在本题中，dp[m][n]表示从起点出发的路径数量，它本身可以从[m-1][n]和[m][n-1]这两个点过来，
因此dp[m][n]=dp[m-1][n]+dp[m][n-1],
因为第一列和第一行的每个点都只有一个路径到达，因此先初始化

70. Climbing Stairs
简单题，也是考虑状态转移方程，相邻状态之间的关系，
一次可以走两步或者一步，
如果最后是走一步，组合数量是dp[n-1],也就是在走n-1步的组合基础上再加一步，追加1，
如果最后走两步，组合数量是dp[n-2],也就是在走n-2步的组合基础上加两步，追加2，
所以 dp[n] = dp[n-1]+dp[n-2]


**85. Maximal Rectangle
把每一层都当作直方图来处理，求直方图的最大矩形面积,卡在了直方图上
refer:
https://www.cnblogs.com/grandyang/p/4322667.html

*87. Scramble String
看到树结构加上字符串组合，就觉得很复杂，其实搞清楚题目意思也挺简单，
判断两个字符串是否符合条件，那就看看能不能劈一刀局部交换得到对方，
两种解决方法，一个是递归，如果两个子串都符合条件那么组合起来的结果肯定也符合，
另外一个是三维动态规划，dp[i][j][k]表示前两个坐标两个字符串的起始位置，最后一个表示长度，局部是否满足条件，
也有很多劈法，只要一种满足条件，那就成立

*95. Unique Binary Search Trees II
毫无头绪，往递归的方向思考了，还是一团乱麻
参考思路划分左右子结点分别递归调用，这样就清晰很多了，用记忆数组来保存中间的遍历结果，减少递归次数，就相当于动态规划了
refer:
https://www.cnblogs.com/grandyang/p/4301096.html

*123. Best Time to Buy and Sell Stock III
状态转移方程的理解，首先理解题意，在n天中最多进行两次交易，求最大利润，
用动态规划的思路解题，两个局部变量local和global,其实可以求出最多k次交易的最大利润，
local[i][j]的含义是在i天内进行j次交易，并且最后一次交易在第i天卖出的最大利润，此为局部最优解
diff = prices[i]-prices[i-1]
local[i][j] = Math.max(local[i-1][j]+diff,global[i-1][j-1]+Math.max(diff,0))
global[i-1][j-1]+max(diff,0)意思是如果第i天的diff小于0，那么交易就变成第i天买，第i天卖，也就是0,
第 i 天卖第 j 支股票的话，一定是下面的一种：

1. 今天刚买的
那么 Local(i, j) = Global(i-1, j-1)
相当于啥都没干

2. 昨天买的
那么 Local(i, j) = Global(i-1, j-1) + diff
等于Global(i-1, j-1) 中的交易，加上今天干的那一票

3. 更早之前买的
那么 Local(i, j) = Local(i-1, j) + diff
昨天别卖了，留到今天卖

global[i][j]的含义是在i天内进行j次交易的最大利润
global[i][j] = Math.max(local[i][j],global[i-1][j])

338. Counting Bits
计算从0到num之间的每个数二进制表示罚中1的个数，简单粗暴，直接遍历，位移运算一位位计算，

**403. Frog Jump
题目没看懂，状态转移方程没理解

*343. Integer Break
拆数字找规律
一种方法是动态规划，从2开始，一个数至少可以拆成两个数，那么遍历所有小于i的数，
一个个拆开组合，dp[i]表示数字i任意拆分得到的最大乘积，dp[i-j]也是如此，
可以推出对于每个待拆分的i,状态转移方程式：
dp[i] = max(dp[i],max(j*(i-j),j*dp[i-j]))
第二种是发现拆分最大值的规律是必然先拆出来所有的3，最后剩2或者4


*139. Word Break
自己的想法是递归调用，但是没处理好导致超时，优化方法是记录s开始的位置递归检测，从前往后，而不是从中间截断两边判断
动态规划关键是搞清楚dp的含义，想清楚状态转移方程，在这里dp[i]的含义是能否截断，
和前面dp[i-1],dp[i-2],....的关系是:
s.substring(i-j,i)是字典中的一个元素
dp[i] = dp[i-j]&&(dict.contains(s.substring(i-j,i)))

reference:
https://www.programcreek.com/2012/12/leetcode-solution-word-break/

198. House Robber
简单题，动态规划的思路是找出状态转移方程，当不知道怎么找出来的时候，自己按照题目要求从头一项一项列出来就容易归纳出来公式
以本题为例，抢劫一排房间，要求是不能抢劫连续的两个房间，否则触发警报被抓，刚开始想的很简单，想当然的觉得就两种情况，
要么全部抢劫单数间即房间号为第1，3，5，7，9....的，或者双数间即第2，4，6，8，10....
其实情况远不止，比如可以是第1，4，6，9...，因为两间相邻的房间选择哪一间不只是与本身的值大小有关还与它们各自相邻的情况有关
所以使用动态规划的方法，我们定义dp[i]是在抢劫第i个房间的情况下的最大值，
下面按照归纳法，
dp[0] = nums[0]
dp[1] = nums[1]
dp[2] = nums[0] + nums[2]
dp[3] = Max(dp[0],dp[1])+nums[3]
dp[4] = max(dp[1],dp[2])+nums[4]
.....
以此类推，递推公式就出来了：
dp[i] = max(dp[i-3],dp[i-2])+nums[i]

还有一种简化方法，不用数组记录状态，两个值即可，
一个是代表抢劫当前房间的情况下的最大值rob
另一个是不抢劫的最大值notrob
那么
rob = preNotRob + nums[i]
notRob = Max(preNotRob,preRob)

refer:
https://www.cnblogs.com/grandyang/p/4518674.html

*213. House Robber II
比198题变化了一个条件，一排房子变成了一个圈，抢了第一间就不能抢最后一间，
所以稍微变化一下就和198题一样，抽成两个子序列1~nums.length,和0～(nums.length-1),
比较这两个子序列的最大值即可

264. Ugly Number II
怎么判断当前最小的数？刚开始是1，很显然接下来是2，之后就不好确定到底是哪个数,
按照uglynumber的定义，之后的数肯定是前面的数乘以2，3，5，但到底是谁呢？
一个办法是记录数组中到第几个数乘2，第几个数乘3，第几个数乘5了，比较它们的大小，谁最小取谁作为序列的下一个数
i2=0;
i3=0;
i5=0;
res[i2]*2,res[i3]*3,res[i5]*5,
取了哪个的乘积，哪个的index就加一，表明它移到下一个数去

我想到的另外一个办法是用小顶堆，一个个弹出来就行了，但是对于数怎么放进去思维不清晰，
参考思路是每次取堆顶的元素分别乘2，3，5再加入堆，弹出n次即可

reference:
https://www.cnblogs.com/grandyang/p/4743837.html


**221. Maximal Square
和最大面积直方图有点像，还是不会，下次去youtube看讲解视频


303. Range Sum Query - Immutable
简单题，毫无难度

*95. Unique Binary Search Trees II
知道递归的思路，实现困难


*96. Unique Binary Search Trees
直觉应该有递推公式，想不出来，原来是卡塔兰数，没听说过，联想95题，其实应该能想出来公式，
刚开始还觉得奇怪为什么95题反而在96题前面，原来如此，通过递归的枚举就知道n和个数的关系了
youtube讲解：https://www.youtube.com/watch?v=GgP75HAvrlY

101. Symmetric Tree
简单题
递归的写法值得参考
refer:
https://www.cnblogs.com/grandyang/p/4051715.html

102. Binary Tree Level Order Traversal
简单题，和101题思路类似，两个list记录每一层的结点，遍历加入即可

222. Count Complete Tree Nodes
和102题一个思路，简单粗暴
二叉搜索树的思想没有体现出来，目前还没想出来

*226. Invert Binary Tree
之前有点傻了，一直纠结用递归的话只能第一层有用，后续的怎么交换，
却没有想到它是结点交换，并非只是值交换，交换的过程中把后续子结点都带过来了
另外一种方法是用队列，先进先出的原则，对队列中的每一个结点的左右子结点做交换，
交换之后再把子结点放入队列以保证子结点的子结点也满足要求
refer：https://www.cnblogs.com/grandyang/p/4790476.html

230. Kth Smallest Element in a BST
广度优先遍历加优先级队列，但是效率不高
另一种方法是中序优先遍历，根据二叉树的性质，左<根<右
又可以分为栈或者递归的方式找到
refer:
https://www.cnblogs.com/grandyang/p/4620012.html
https://www.cnblogs.com/yrbbest/p/4999289.html

235. Lowest Common Ancestor of a Binary Search Tree
没有思路，看到参考解法，利用了BST的性质，缩小搜索范围从而找到LCA，


337. House Robber III
打家劫舍系列，没有处理好连续两个结点不抢的情况,
对抢劫结点理解有歧义，以为是一层层的整体抢，不知道其实左右子结点抢的结点可以不是同一层同时抢
解法同样是递归
refer:
https://www.programcreek.com/2015/03/leetcode-house-robber-iii-java/


*404. Sum of Left Leaves
看起来挺简单的，但是用栈做中序遍历不能区分当前叶子结点是否为左结点导致出错
解决策略是入栈时用当前结点的左叶子结点相加，也可用队列
另外一种方法是递归，本质也是加当前结点的叶子结点
refer:
https://www.cnblogs.com/grandyang/p/5923559.html

437. path sum III
也是递归，为0返回的情况不够周全，抽离出来一个递归函数处理比较好
一个函数是以当前结点为根结点，另外一个是子结点递归
refer:
https://www.cnblogs.com/liujinhong/p/6444322.html

*449. Serialize and Deserialize BST
再次体会了递归的妙用，序列化过程中采用前序遍历，根->左->右，递归写入string
非序列化还原的过程中也是递归，根结点先出来，递归还原左子结点，再递归还原右子结点，
用一个链表队列保存顺序

450. Delete Node in a BST
处理不好要删除的结点左右子结点都存在的情况
解决方案一，递归调用，分情况讨论，
第一种情况是被删除结点为叶子结点，那么直接赋值为空即可，
第二种情况是只有左子结点或者右子结点，那么就把它的父结点直接指向子结点即可
第三种情况是同时存在左右子结点，需要在右子结点中找最小值，
也就是左子树的最左叶子结点，然后把它的值赋给父结点，

513. Find Bottom Left Tree Value
广度优先，层序遍历解决

7. Reverse Integer
简单题，主要是要注意边界条件，判断方法是当前结果是否超过上限除以10，或者上限减去余数除以10是不是小于当前结果，这两种情形来判断会不会越界的问题

9. Palindrome Number
简单题，简单粗暴的转成字符串判断，效率不够高

29. Divide Two Integers
本来以为很简单，一直减下去好了，但是由于上下限不一致的原因，比较啰嗦，然后考虑了特殊情况也超时了
参考解法用指数加快计算速度，当前的除数一直二倍下去记录，直到超过被除数
reference：
https://kingsfish.github.io/2017/10/11/Leetcode-29-Divide-Two-Integers/

43. Multiply Strings
根据乘法的错位相加特性，可以从最后一位往前推，计算每一位数的值，
每一位数的值保存在数组中，进位需要的时候拿出来相加即可
前面很多零的处理办法是检测当前字符串是否为空，
为空说明还在最前面，跳过，中间的零则需要放进来

*50. Pow(x, n)
解法一是递归，
解法二是指数级收缩，和自己开始的想法类似，不过得反着来
refer：
https://www.cnblogs.com/grandyang/p/4383775.html


**60. Permutation Sequence
根据全排列的顺序找出结果，先找规律再实现，
思路有了不会实现
refer：
https://blog.csdn.net/zgljl2012/article/details/72625433

*69. Sqrt(x)
虽然标的是简单题，想到的解法是二分查找，但是写的很丑，效率不高，
前面提交一直不通过是因为除以2取整可能会舍弃边界值，导致缩小范围过多，正好漏掉了答案
牛顿迭代法，思想一样，但是思路更清晰，实现简洁
refer：
https://www.cnblogs.com/grandyang/p/4346413.html

*149. Max Points on a Line
两点共线的方程式为kx+b,k=(y1-y2)/(x1-x2),b=y1-kx,
因为除法可能导致k为浮点数，斜率不准，所以求出(y1-y2)和(x1-x2)的最大公约数便于约分
又因为从同一点开始相连，所以不存在斜率相等的两条平行线，所以不用考虑截距b
求最大公约数用更相减损术


*166. Fraction to Recurring Decimal
想的挺简单，重点处理循环小数，用map检测循环，但是对于循环位置处理不好
自己用的是int类型，对于能除尽的小数处理啰嗦，再就是long类型的，
map的value记录当前值的结果在字符串中的位置，便于后续插入


168. Excel Sheet Column Title
简单题，递归搞定，根据题意可知，1-26对应A-Z，观察规律，27是AA，也就是27/26和27%26，
然后考虑特殊情况Z，如果n是Z的倍数，那么字符串肯定是以Z结尾，所以每次递归的时候带上后缀
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    29    AC

171. Excel Sheet Column Number
简单题，基本思路和167一样，这两道题实质是一样的，也是递归，不过是还原，相当于26进制

*172. Factorial Trailing Zeroes
想到了实质是求5的个数，不用递归不好实现

202. Happy Number
简单题，同样是递归求值，加上一个set记录已经计算过的值避免死循环

1305. All Elements in Two Binary Search Trees
解题思路，中序遍历加优先级队列即可，
不快的原因在于没有利用二叉树的性质，每个结点的值遵循左中右依次递增的规律，
所以遍历数组之后可以合并两个有序数组，加快速度,经验证提高了一点点，前者40ms,后者29ms
refer:
https://www.cnblogs.com/qinduanyinghua/p/12119711.html



 {'$or': [{'_id': 973}, {'user_id': 973}]}

  {"$or": [{"_id": 889}, {"user_id": 889}]}


1054. Distant Barcodes
直觉不难，但是写不出来，看了这个博客醍醐灌顶，思路清晰，简单的把最高频数字依次分组加入
https://leetcode.jp/leetcode-1054-distant-barcodes-%E8%A7%A3%E9%A2%98%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90/

1046. Last Stone Weight
题目大意是每次挑两块最大的石头相撞，相同的话剩余0，这两块石头同归于尽，在数组中体现为0，
不想等的话为两者的差值加入数组中，
所以思路是排序找出最大的两个值，然后根据它们的情况判断，
剩下的值以及原数组的其他值都加入到新数组中，递归调用即可

**882. Reachable Nodes In Subdivided Graph
题目意思没看懂，参考大神的博客之后，可以理解题意为无向图，N个顶点，可以从任意结点出发走M步能到达的结点数量
要注意的是每个边上的结点，走过的结点也不能再走了
看到的解法是BFS，Dijkstra Algorithm,当前能到达的结点遍历，
关键点在于while循环，处理不能达到另外一个结点时的两个结点之间的子结点
【
在 while 循环中，首先取出堆顶元素数对儿，分别取出步数 move，和当前结点编号 cur，此时检查若该结点已经访问过了，直接跳过，否则就在 visited 数组中标记为 true。此时结果 res 自增1，因为当前大结点也是新遍历到的，需要累加个数。然后我们需要遍历所有跟 cur 相连的大结点，对于二维数组形式的邻接链表，我们只需要将i从0遍历到N，假如 graph[cur][i] 为 -1，表示结点 cur 和结点i不相连，直接跳过。否则相连的话，两个大结点中小结点的个数为 graph[cur][i]，此时要跟当前 cur 结点时剩余步数 move 比较，假如 move 较大，说明可以到达结点i，将此时到达结点i的剩余步数 move-graph[cur][i]-1（最后的减1是到达结点i需要的额外步数）和i一起组成数对儿，加入最大堆中。由于之前的分析，结点 cur 往结点i走过的所有结点，从结点i就不能再往结点 cur 走了，否则就累加了重复结点，所以 graph[i][cur] 要减去 move 和 graph[cur][i] 中的较小值，同时结果 res 要累加该较小值即可
】

refer:
https://www.cnblogs.com/grandyang/p/11074953.html
https://blog.csdn.net/weixin_30555125/article/details/98930104

871. Minimum Number of Refueling Stops
动态规划没有想出来状态转移方程，堆没有思路
动态规划的关键点在于想出来状态转移方程的意义，或者说dp[i]的含义，如果dp[i]代表加了i次油能到达的距离，那么问题迎刃而解
堆的解法是把所有能到达的点都扔进去，每次取最大的看能到多远,太妙了，直接就选出了加油量能达到最大的点
refer:
https://www.cnblogs.com/grandyang/p/11186533.html

*786. K-th Smallest Prime Fraction
题目中的数组为质数数组，暴力破解行不通，通过分数的规律，分子大或者分母小则分数大，
毫无疑问最小的分数为第一个和最后一个元素的组合，至于后续是第二个和最后一个元素组合还是第一个和倒数第二个分数组合那就不知道了
那就把这两个都放进去，通过小顶堆弹出最小值的过程，不断把比它稍大的可能值放进去排序，大大减少多余计算
http://bookshadow.com/weblog/2018/02/18/leetcode-k-th-smallest-prime-fraction/


*218. The Skyline Problem
天际线问题，看起来有点眼熟，开始的想法是把二维数组变成一维数组，左侧右侧及高度
后来发现对于有交集的多个间隔区间很难处理
参考博主思路，把左侧右侧及高度分开对应，右侧高度处理为负值，便于区分，
放入queue中根据左侧坐标及高度排序，两个queue，一个左侧对应高度排序，一个高度排序，遇到正值就加入，负值则弹出
refer：
https://blog.csdn.net/katrina95/article/details/79178168

*313. Super Ugly Number
我想到的解法是，队列加入可能的最小值，每次取出来最小值和数组中的元素依次相乘得到可能的最小值
但是超时了，因为有很多不必要的计算
看到的改进解法是用数组记录最小值排序，同时用指针在这个数组中移动，每次都取最小值，
然后计算接下来的可能的最小值中进行比较，选择最小值

295. Find Median from Data Stream
一年前提交了很多次没通过，现在终于过了，题目挺简单的，注意在除之前把数字转换成double类型，不然小数点后面的数会被舍弃

264. Ugly Number II
现在更加理解了这道题的精髓，核心在于2，3，5每次相乘的数是最小的，但是有没有比其他数小不知道，所以当它们与最小值相乘时不是当前最小要保留，
index指针来记录它们已经与第几个数相乘了，但是并非当前最小的，一直在等待，快慢进度不一样，直到被选择，才往下一个最小的值那里走，往复循环

355. Design Twitter
题目不难，不知道为什么总是有一个多余重复的数

*719. Find K-th Smallest Pair Distance
第一种解法是利用条件，统计所有距离的个数，然后从零开始相加统计个数，相对优先级队列节省了空间，但是时间也是n平方，不知道为什么可以
第二种解法是二分查找，似懂非懂，没搞懂怎么计数的
refer:
https://www.cnblogs.com/grandyang/p/8627783.html
  
767. Reorganize String
借鉴了rearrangeBarcodes的分组排列思想，把出现频率最高的字母分到不同的组，依次分配
再重新组合检测相邻的是否相同即可


703 Kth Largest Element in a Stream
挺简单的题开始没想清楚，想到了维持K大小的队列，但对于队列元素的管理没有想到，
可以利用小顶堆，堆顶元素最小的特点来进行排序，把元素加入队列，当队列大于k的时候把堆顶的元素也就是最小的弹出，那么剩下的肯定是最大的k个，
此时堆顶元素就是第k大了，开始还傻乎乎的用大顶堆弹出第k个元素，一直苦恼于前面的元素怎么办
refer:
https://www.cnblogs.com/grandyang/p/9941357.html

319. Bulb Switcher
根据题意每一轮每隔几个灯泡开关相反，完全按题意实现，超时，
参考方案发现灯泡最终状态的规律为完全平方数，大大减少计算量
https://www.cnblogs.com/grandyang/p/5100098.html

326. Power of Three
简单题，判断一个数是不是3的幂次方，注意小于零的情况

335. Self Crossing
没搞清楚题意，感觉不难，下次再来
refer：
https://www.cnblogs.com/grandyang/p/5216856.html

*365. Water and Jug Problem
和一个脑筋急转弯的题目很像，现在是抽象成一个普遍问题，
根据网上的解法，z=mx+ny,z是容器中要量出来的水，x是往外舀水，y是往容器里灌水，
根据贝祖定理，对于ax+by=sd,若a,b为整数，且d=gcd(a,b),那么对于任意的x,y,ax+by一定是d的倍数
https://www.cnblogs.com/grandyang/p/5628836.html

367. Valid Perfect Square
开始的想法是从一半往缩小的方向找，步长为1，超时；
改进的想法是二分查找，用的递归，边界没有处理好，参考解法也是递归，一个while循环搞定
第二种解法是从1开始遍历完全平方数，看有没有符合条件的
第三种方法是以指数级缩小范围，从x/2到x之间的遍历，缩小遍历范围，

**372. Super Pow
第一次听说快速幂算法，还不清楚证明过程
refer:
https://blog.csdn.net/beyond702/article/details/53222077

*368. Largest Divisible Subset
动态规划，dp[i]为到i的最大子集长度，再来一个数组保存下标 
https://www.hrwhisper.me/leetcode-largest-divisible-subset/

*396. Rotate Function
轮询计算，刚开始也是直接按照题意计算，但是超时了，
参考博主的解法，发现轮询的规律，
sum =  1A + 1B + 1C + 1D
F(0) = 0A + 1B + 2C + 3D
F(1) = 0D + 1A + 2B + 3C = F(0) + sum - 4D
F(2) = 0C + 1D + 2A + 3B = F(1) + sum - 4C
F(3) = 0B + 1C + 2D + 3A = F(1) + sum - 4B
可以归纳出，F(i) = F(i-1) + sum - nums.length*nums[nums.length-i]

400. Nth Digit
1-9 x=n
10-99 9+2x=n
100-999 9+90*2+3*x = n
1000-9999 9+90*2+3*900+4*x=n
思想是类似的，关键是怎么避免数字超过上限的问题
refer:
https://blog.csdn.net/MebiuW/article/details/52575028

413. Arithmetic Slices
没读懂题意，大意是在数组中找等差数列，三个连续的数字差相等即为等差数列，子数列也算
https://www.cnblogs.com/grandyang/p/5968340.html

423. Reconstruct Original Digits from English
zero 0
one 1
two 2
three 3
four 4
five 5
six 6
seven 7
eight 8
nine 9
数字英文字母打乱顺序，要求重组成数字，按字母顺序
经过观察，首先筛选出特殊的数字，
比如只有8包含g,只有6包含x,只有4包含u,只有0包含z
把这几个数字筛选过后发现只有4和5包含f
....
类似的，筛选字符串的所有数字，刚开始是一个字母一个字母的去除，超时
后来想到了分组统计，利用一个27的数组记录每个字母的出现次数，每筛选出一个数字，直接减去它就计数了

34. Find First and Last Position of Element in Sorted Array
二分查找即可
参考博主先找左边界，再找右边界
refer：
https://www.cnblogs.com/grandyang/p/4409379.html

33. Search in Rotated Sorted Array
s=数组中有两个有序序列，但是不知道第二个的起点在哪里，
怎么判断第二个起点在左半边还是右半边呢，取三个点，左，中，右，根据规律
首先判断出左右两边哪个完全有序，找出有序的，看目标值是否在此范围，缩小查找范围
递归调用或者迭代均可，缩小查找范围
refer:
http://bangbingsyb.blogspot.com/2014/11/leetcode-search-in-rotated-sorted-array.html

*31. Next Permutation 
没读懂题意，经过博主讲解，题意是找出从小到达排序的下一串数字
根据下一串数字的规律，如果给定的数字串是降序的，那么下一个就回到第一个排列（也就是最小的组合），
不然的话，从末尾往前看数字逐渐变大，找到第一个不符合此规律的数字，再从这个位置往后找找到第一个比它小的数字交换，再从小到大排序
1 2 3 4 7 8 0 5 9
refer:
https://www.cnblogs.com/springfor/p/3896245.html

162. Find Peak Element
这道题有点摸不着头脑，没什么难度，直接遍历判断是否满足条件就好了，
要是都不满足条件，直接返回最大值
根据博客解说，了解了其他解法，可以检测递增序列，第一个不满足的就是峰值，或者在左右两侧追加值，这样递增或者递减序列也能判断
还有一种就体现了题目的tag，二分查找，折半找峰值，关键点在于mid和mid+1比较，判断峰值在左侧还是右侧

275. H-Index II
感觉挺简单，硬是想不出来，这道题的本质在于动态值的情况下怎么做二分查找
题意是发表的文章满足n篇文章都有n以上的引用次数，citations[i]>=length-i
怎么判断比较快呢，条件是citations[mid]==length-mid
https://www.cnblogs.com/grandyang/p/4782695.html

278. First Bad Version
简单题，最普通的根据条件折半查找

925. Long Pressed Name
简单题，两个字符串比较，重复的一直往前走

977. Squares of a Sorted Array
简单题，直接排序


*424. Longest Repeating Character Replacement
开始读不懂题意，后来看网上博客算是搞懂了，一串字符串，最多替换k次，问最长的相同字符字串有多长
解题思路是滑动窗口，一个长度为26的数组记录每个字符在滑动窗口内的出现次数,窗口左边收缩右边扩张，
左边收缩时数组对应的字符个数减一，每次向右扩张时与当前最大值比较,并计算窗口大小，
如果窗口长度和最大值之差小于等于替换值的话可以更新最大值为窗口长度
refer:
https://www.cnblogs.com/reboot329/p/5968393.html

*457. Circular Array Loop
没看懂题目

524. Longest Word in Dictionary through Deleting
简单粗暴直接上，先把数组按照字符串长度逆序比较再去字符串里面找
refer:
https://www.jianshu.com/p/f1a2b52854ef

287. Find the Duplicate Number
简单题，效率不高

*388. Longest Absolute File Path
最长的绝对文件路径，关键是把握好分界线标志，文件和文件夹的区别在于是否包含.,
再者没有注意到除了根目录外之后的子目录都是一路到底，注意到这一点就好解决了，
那么把每一段切割开来判断，对于每一段透过\t,可以得到文件或者文件夹的名字，若为文件，
更新最长路径值,map记录每一层的文件夹的绝对长度
refer:
https://www.cnblogs.com/grandyang/p/5806493.html

*683. K Empty Slots
题目大意是在某一天是否存在一个以左右为边界，中间不开花，且长度为k的区域
基本思路是遍历判断是否满足条件，参考博客三种思路，
？解法一，额外一个数组按天数记第几天哪盆花开，看看每隔k天，两个花槽之间有没有更早的天数，
refer:
https://blog.csdn.net/katrina95/article/details/79070941

*681 Next Closest Time
题意很容易懂，就是找接下来的时间点，数字只能从给定的时间选择
第一种思路是，数组记录出现过的数字，同时找出最小值，再一位一位的确定值，
确定方法是去数组里面找有没有比当前值大的，有的话直接替换返回，没有，则把当前值重置为最小值
第二种办法是，找出这四个数字的所有排列组合比较差值，深度优先遍历求解DFS

https://blog.csdn.net/katrina95/article/details/79081787

482. License Key Formatting
简单题，从后往前遍历判断组合计数

*686. Repeated String Match
没有想出来A重复多少次好，解决方法是当A的长度小于B时一直重复添加A，如果A不包含B,再加上A，还不包含，那就是找不到了;
另外一种简洁的方法是，想清楚A最多重复多少次，其实是B/A+2次，那么循环遍历A的重复结果检测是否包含B即可
https://www.cnblogs.com/grandyang/p/7631434.html

346. Moving Average from Data Stream
锁住的题，看着不难

340 Longest Substring with At Most K Distinct Characters
最多k个不同字符的最长子串，很简单的一道题，久了不练生疏了，直接map加一个记录子串的起始位置的变量遍历解决问题

308 Range Sum Query 2D - Mutable
矩阵可变怎么处理？
一个是更新不可变每个位置（从零点开始到此位置的矩阵）和的值，
一个是转变思路，不再维护每个位置的和，而是维护每一列的和，这样更新的时候只影响某一列

418 Sentence Screen Fitting
不是很难，搞懂题意，也就是把单词组成的句子按顺序排列，每行有长度限制，遍历即可

*281 Zigzag Iterator
之字形迭代器，其实就是每个数组按顺序抽元素组合，可以利用迭代器本身的性质，关键点在于确定元素在哪一个数组中，index的计算是关键，
看数组有几组，参考博客的巧妙解法是生成迭代器数组，再去确定位置
refer:
https://www.jianshu.com/p/d0f5502d8d3a

*298 Binary Tree Longest Consecutive Sequence
简单的DFS递归调用，不太熟练
refer:
https://www.cnblogs.com/yrbbest/p/5047038.html

394. Decode String
一个栈解决问题，效率不高

**753. Cracking the Safe
题目看懂一半，n位密码，0-k之间的数字，问包含所有数字组合的万能钥匙最短长度
参考解法，从0开始往上加，已有的放到set做记录，遍历求解；
第二个java版本的求解，解释太高级了，反而看不懂了，解说中提到的视频可以看看
refer:
https://www.cnblogs.com/grandyang/p/8452361.html
https://github.com/cherryljr/LeetCode/blob/master/Cracking%20the%20Safe.java

*393. UTF-8 Validation
没有理解utf-8的编码规则，题目也没读懂


*361. Bomb Enemy
我的想法是只记左上方，确实是有问题，右下方漏掉了，指望累计可以加进来，不知道有没有问题
参考解法一是四个数组，分别记录四个方向，左右上下，
参考方法二节省了空间，按行记录敌人数量，没看懂
refer:
https://www.cnblogs.com/grandyang/p/5599289.html


506. Relative Ranks
简单题，效率不高，用的是优先级队列，根据index对应的值给index排序，再生成结果赋值

849. Maximize Distance to Closest Person
简单题，空间复杂度还可以优化

**847. Shortest Path Visiting All Nodes
初步的想法是深度优先遍历，把最长的留到最后，前面的随意，基本上就是最长的深度+加上其他乘以2
参考思路，广度优先和动态规划是求极值的利器，还没有吃透
refer:
https://www.cnblogs.com/grandyang/p/11410007.html

840. Magic Squares In Grid
简单题，判定条件比较琐碎，也是空间复杂度效率不够

**493. Reverse Pairs
这道题挺有意思的，题目很好懂，条件也挺简单，就是i>j,nums[i]>2*nums[j]
初步的想法太naive了，直接把条件摆进去遍历不就得了么，首先卡在了2*nums[j]超过整形数字的上限上面，解决办法是改成nums[i]-nums[j]>nums[j],
然而时间复杂度是n平方，超时；优化方向可能是避免重复计算，那可以猜测是从后往前？
参考博客确实是从后往前遍历而且利用了树状数组的特性计数，树状数组还没有掌握
分割重现关系没看懂
refer:
https://www.cnblogs.com/grandyang/p/6657956.html

*839. Similar String Groups
算不上难题，但没搞懂分组的意思，并不是相似就相加，而是调换顺序之后是同一个单词的为一组，
参考解法BFS活着DFS，
DFS,按照惯例，递归调用，一个set作为visited记录有没有访问过，isSimilar这个方法写的好，题目已经说了单词是异构体，那么不同之处一定是2，才满足，其他的都不算，按此计数即可
BFS则是借助queue记录，把DFS的递归化用到一个方法中来，其实也是每次需要遍历标记，
第三种方法是联合查找，对于群组归类问题都可以用联合查找，已经熟悉了一些，把所有单词的根找到，根相同即为一组，统计根的数量即为组的数量
refer:
https://www.cnblogs.com/grandyang/p/11503433.html

515. Find Largest Value in Each Tree Row
BFS,层序遍历可以解决很多问题，可惜效率不够高[T48%,M6.45%]
参考博客的解决方案，
一个是层序遍历，把记录当前层节点的list换成queue,那怎么确定是这一层呢，
很简单，每次循环添加下一层节点之前记录当前queue的大小，就是这一层的节点数量；[T48%,M6.45%],效率没变化
第二个是用递归,用一个参数记录当前深度,深度其实也直接和返回结果的size有关联，问题迎刃而解,[有个问题是改变list最后一个值，递归的时候会出问题，由于没有锁]
refer:
https://www.cnblogs.com/grandyang/p/6417826.html

*529. Minesweeper
扫雷游戏，按规则翻牌，看起来也不难，卡在了自动掀起那个地方，(0,2)那个位置为什么没触发，因为周围不是空白，不会自动掀起，
所以按规则实现程序，注意到参考程序递归的一个条件是当前点为‘E',即未掀起状态，才会递归到周围去标记，那么就好理解为什么（0，2）还是初始状态了

[['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'M', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E']]

Click : [3,0]

Output: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

cn343. 机器人运动
看起来挺简单，遍历检测就好了，理解有偏差，从（0，0）出发，首先要能到这个点，
然后四个方向运动，把每个方向能到的点递归相加，我写的是每个方向单独行动了，但是不知道哪里出错了，总是要少一点，估计是计数没处理好，visited标记，
refer:
https://blog.csdn.net/u011080472/article/details/51295322

cn191.二进制中1的个数
<<<表示无符号的位移


cn50.数值的整数次方
思路有了，想节约计算时间，提高效率，那就用指数，但实现很糟糕，while循环计数没处理好，
参考思路用递归，指数幂减用位移操作，很巧妙的解决了奇偶数的问题
refer:
https://blog.csdn.net/jsqfengbao/article/details/47164537  

cn10.正则表达式匹配
没有考虑全所有情况
参考博客，递归非递归的都可以
refer:
https://www.programcreek.com/2012/12/leetcode-regular-expression-matching-in-java/

**854. K-Similar Strings
不知道怎么应用BFS，先抄一遍，set记录有没有访问过这个字符串，queue记录变换的中间状态遍历比较
refer:
https://www.cnblogs.com/grandyang/p/11343552.html

*815. Bus Routes
题目好懂，觉得自己能实现，还是差点火候，刚开始想的是用图搜索，没有处理好站点和车次的关系


面试题21. 调整数组顺序使奇数位于偶数前面
确实是简单题，开始的想法是两个指针，一个发现偶数，一个发现奇数，不合要求的调换，想的太复杂了，处理起来会导致交换之后死循环，
其实抓住一点，奇数在偶数前，那么前面的是奇数，一个记录从0开始的连续奇数序列的最后一个位置，一个记录当前奇数的位置，只要和连续的接下来一个位置调换即可
讨论区的一个思路和这个类似，不过是从后往前遍历，遇到奇数就放到最前面，保证了前面都是奇数
 public int[] exchange(int[] nums) {
        //思路类似于荷兰国旗 
        if(nums.length==0||nums.length==1) return nums;
        int i=0,j=nums.length-1;
        while(i<j){
            if(nums[j]%2==1){
                int temp = nums[i];
                nums[i++] =nums[j];
                nums[j] = temp;
            }else{
                j--;
            }
        }
        return nums;
    }

25. 合并两个排序的链表
很简单的题，久了不做手生，递归迭代都可以

cn101. 对称的二叉树
待优化

面试题33. 二叉搜索树的后序遍历序列
根据二叉树的特点还原成树再判断？

cn113. 二叉树中和为某一值的路径
注意递归查找过程中元素的处理，回溯到不同节点需要进行删除操作，保存结果拷贝当前list状态

面试题26. 树的子结构
对于陌生题的一个技巧就是从特殊到一般，归纳规律，一一解决


cn295. 数据流中的中位数
时间效率待提高，参考思路大顶堆小顶堆数量比较选出中位数很好

优先级队列实现小顶堆，为什么容量参数没生效
Queue<Integer> queue = new PriorityQueue<>(k);


cn426. 二叉搜索树与双向链表
不知道数据结构怎么组织，方法基本上是中序遍历

cn297. 序列化二叉树
都通过BFS搞定，注意空值问题

*cn235 - I. 二叉搜索树的最近公共祖先
二叉搜索树，注意利用它左小右大的性质，跌倒好多次

面试题46. 把数字翻译成字符串
待优化, 可优化为递归

cn400. 数字序列中某一位的数字
边界问题处理不好


面试题51. 数组中的逆序对
超时

面试题52. 两个链表的第一个公共节点
待优化, 双指针没看懂

面试题54. 二叉搜索树的第k大节点
假设，你花了点时间，练习了二叉树的三种遍历方式： a. 前序遍历 b. 中序遍历 c. 后续遍历

你也学习了二叉搜索树，深入研究了二叉树搜索树的特性，并且深刻知道二叉搜索树的一个特性：通过中序遍历所得到的序列，就是有序的。
待优化, 可优化为递归,根据二叉搜索树的性质，右>中>左，递归到第k大即可停止


cn110 - II. 平衡二叉树
求高度递归直接破题

*面试题56 - I. 数组中数字出现的次数
关注异或操作的应用

*面试题56 - II. 数组中数字出现的次数 II
考察位移操作

cn239 - I. 滑动窗口的最大值
滑动窗口还没有掌握

面试题57 - II. 和为s的连续正数序列
猜递归，但是写不出来

面试题59 - II. 队列的最大值
还是滑动窗口

面试题60. n个骰子的点数
居然可以用动态规划

面试题62. 圆圈中最后剩下的数字
约瑟夫环没掌握

200. Number of Islands
岛屿数量终于解决，搜索方式深度优先，
只要发现一个点是岛屿，那么与它相邻的点就继续搜索下去，一路标记，
开始按顺序遍历的问题是有些相邻的点并不是按搜索顺序渲染的，所以发现一个点符合要求要用DFS一直渲染下去
空间效率优化方案，可以通过改变grid值实现，那么就不需要visited标记了,效果不太明显

207. Course Schedule
DFS，理解还是有偏差,思路大致相同，标记访问过的，状态可以用三个数表示，0未访问，1走得通，-1当前遍历已走过的路，遇到了说明成环行不通

329. Longest Increasing Path in a Matrix
DFS, 还差一点点，用一个二维数组记录搜索过的路径最大值，减少搜索时间


36. Valid Sudoku
比较简单，按照规则来就好了，满足横纵九宫格不重复即可，
学会了Lis<Integer>[] test = new List[n], Lis<Integer>[][] test = new List[n][n]的写法，


37. Sudoku Solver
在36题的基础上，每填入一个数字验证是否为有效九宫格？
效率有点低,参考博客的改进是只验证当前加进去的这个数字是否满足条件就好了，算出每个九宫格的起始坐标也是有公式的，(i-i%3,j-j%3),一行行的填数字验证
refer
https://www.cnblogs.com/grandyang/p/4421852.html

39. Combination Sum
递归搜索满足条件的元素，注意递归时数组遍历开始的位置


44. Wildcard Matching
和正则匹配差不多，以为十拿九稳，还是挂了
可以直接从两端开始，也可以动态规划，递归回溯
https://www.cnblogs.com/grandyang/p/4401196.html
完美体现递归回溯，当前结果依赖于后面的结果，决定最终结果
https://leetcode.com/problems/wildcard-matching/discuss/510552/Simple-Java-Recursion-Memorization

46. Permutations
开窍了就简单了，回溯和递归相关联又不同，回溯需要标记走过的路，减少重复，递归出口是基本条件

47. Permutations II
在46的基础上加了重复元素，简单的改进是在46的基础上加上元素是否已存在的检测，已存在则不加入结果集，效率不够高；
参考讨论区的优化方案，它的思路是在原有数组的基础上不动，再交换各个元素的位置，形成排列组合，
https://leetcode.com/problems/permutations-ii/discuss/523257/Java-clean-backtracking-beats-99-with-reasoning

*51. N-Queens 
接近做出来了，对皇后的势力范围理解有误导致出错，
她是在车的基础上加上斜线势力范围，而非九宫格,递归循环那里是一层，而非两层，每一行一个循环，不需要再加循环每行

52. N-Queens II
实际上在51的基础加了一个问题，不需要返回结果，直接把51的结果取size即可，不知道还有什么别的妙招

77. Combinations
简单题，递归回溯，记得进去的元素处理完了要出来，一样的思想

78. Subsets
子集的各种组合，77题稍微变形

*79. Word Search
原理也是一样，这里犯的错是访问过的点在递归回溯过程中有些点的状态没有还原，
不知道怎么还原,后面添加了恢复状态，中间态没还原，是因为在递归回溯的状态下，不管对错都返回结果了，导致行不通的路径中间状态不能还原
所以必须注意中间状态的还原

思路类似，这个方法节省了空间，它把走过的位置值改变了，这样即使走过的路值和后来的一样也不会相等了
https://leetcode.com/problems/word-search/discuss/550443/java-backtracking
思路和上面参考链接一样，能快这么多？
https://leetcode.com/problems/word-search/discuss/547970/Java-solution-using-trivial-DFS-beats-99.91

*60. Permutation Sequence
老题了，也看过很多次解题方法，大概知道前面递增和后面遇到的第一个递减的交换位置，还是写不出来
refer
利用排列规律推算，一步到位
https://www.cnblogs.com/grandyang/p/4358678.html
看到另外一个例子，茅塞顿开，其实和77很像，按顺序递归回溯天然就是从小到大排序的
https://leetcode.com/problems/permutation-sequence/discuss/534032/Java-permutate-till-k

*89. Gray Code
换汤不换药的递归回溯，思路零散，翻转想到了，怎么递归没想到,
解题思路也是递归，依次翻转
https://leetcode.com/problems/gray-code/discuss/542067/Java-2ms-dfs-slow
感觉这个方案像掩码计算，直接出结果
https://leetcode.com/problems/gray-code/discuss/519075/Java-0ms-100-with-Explanation

*90. Subsets II
依然没有学会对重复元素的优雅处理方案，简单跳过是不行的,参考方案有的情况加重复元素，有的不加
https://leetcode.com/problems/subsets-ii/discuss/545255/Java-oror-99.76-time-oror-New-Approach

93. Restore IP Addresses
递归查找，注意边界和极端情况（0000，1111，00100）


*126. Word Ladder II
题目写起来不难，不知道为什么答案只是一部分，看到别的博主答案是找最短路径，属于BFS，那么递归还合适吗，这应该是DFS了

[["hit","hot","dot","dog","log","cog"],
["hit","hot","dot","dog","cog"],
["hit","hot","dot","lot","log","dog","cog"],
["hit","hot","dot","lot","log","cog"],
["hit","hot","lot","dot","dog","log","cog"],
["hit","hot","lot","dot","dog","cog"],
["hit","hot","lot","log","dog","cog"],
["hit","hot","lot","log","cog"]]

[
["hit","hot","dot","dog","cog"],
["hit","hot","lot","log","cog"]]

路径是有记忆的，BFS用map记录每个word的高度，减少递归时间,再DFS搜索，我实现的时候记录了搜索到目前的最小高度，已经接近了
https://blog.csdn.net/MebiuW/article/details/53165141

131. Palindrome Partitioning
认真读题，搞懂意思就很容易下手了，虽然效率还不够

*140. Word Break II
合成词卡住了，map改成<string,<string>>,新思路trie tree
refer:
https://www.cnblogs.com/grandyang/p/4576240.html

*211. Add and Search Word - Data structure design
直觉trie tree效率高，普通的递归搜索效率低
https://leetcode.com/problems/add-and-search-word-data-structure-design/discuss/550523/Java-classic-Trie-and-recursive-solution

*306. Additive Number
想法类似，还是没实现,离成功只差一点点，最开始的两个数比较特殊单独处理，其他递归
https://www.cnblogs.com/grandyang/p/4974115.html

*357. Count Numbers with Unique Digits
傻了，一直想的是计算重复的，干嘛不直接排列组合呢，瞬间容易很多
refer：
https://www.cnblogs.com/grandyang/p/5582633.html

401. Binary Watch
简单题，差点卡住，本身是按顺序往后组合，不必标记变化数组了

784. Letter Case Permutation
简单题，有优化空间，递归遍历即可

**980. Unique Paths III
思路类似，不知道错在哪里
https://www.cnblogs.com/qinduanyinghua/p/11518618.html

1307. Verbal Arithmetic Puzzle
字母数字交织，一时间不知道按数字遍历还是按字母遍历，
开始想的是按数字遍历，有个问题就是字母怎么分配这些数字，中间态其他字母怎么变动，很麻烦
参考博主的思路，按字母分配数字，没出现的跳过，最后一起加，计算，安排的明明白白，大道至简，诚不我欺
https://leetcode.jp/leetcode-1307-verbal-arithmetic-puzzle-%E8%A7%A3%E9%A2%98%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90/

*1239. Maximum Length of a Concatenated String with Unique Characters
没看懂题目的样子

1219. Path with Maximum Gold
简单题，每个方向搜索，取最大的结果

*687. Longest Univalue Path
简单题，老是错，根本原因是没读懂，这道题是求两个val相等的节点之间最长的路径是多少
refer:
https://www.cnblogs.com/grandyang/p/7636259.html

*698. Partition to K Equal Sum Subsets
差那么一点点，数组分组，所有元素都参与的递归，for循环递归位置搞错了
https://www.cnblogs.com/grandyang/p/7733098.html


*726. Number of Atoms
递归哪一步想清楚
https://blog.csdn.net/katrina95/article/details/99947645

1137. N-th Tribonacci Number
简单题，和斐波那契数列数列一样，不用数组记录历史结果就超时

938. Range Sum of BST
简单题，根据二叉搜索树的性质递归查找符合条件的元素


894. All Possible Full Binary Trees
不难，想清楚以后递归，下面这个解法写的太啰嗦，但思路应该是对的，不知道什么地方错了
  public List<TreeNode> allPossibleFBT(int N) {
      TreeNode root = new TreeNode(0);
      List<TreeNode> res = allPossibleFBT(root,N);
      return res;
    }


   public List<TreeNode> allPossibleFBT(TreeNode root, int N) {

      List<TreeNode> res = new ArrayList<>();
      if(N==1){
        res.add(root);
        return res;
      }
      
      for(int i=1;i<=N-1;i=i+2){
        TreeNode left = new TreeNode(0);
        TreeNode right = new TreeNode(0);
        List<TreeNode> left_all = allPossibleFBT(left,i);
        List<TreeNode> right_all = allPossibleFBT(right,N-1-i);
        List<TreeNode> all = getCombination(root,left_all,right_all);
        res.addAll(all);
      }
      return res;
    }

  public List<TreeNode> getCombination(TreeNode root,List<TreeNode> left_all,List<TreeNode> right_all){
      List<TreeNode> res = new ArrayList<>();
      for(TreeNode left :left_all){
        for(TreeNode right:right_all){
          root.left = left;
          root.right = right;
          res.add(root);
        }
      }
      return res;
  }

*794. Valid Tic-Tac-Toe State
没有思路，题目意思理解得也有点问题，问的是当前游戏是不是一个有效状态
看了解题，和递归也没什么关系
https://www.cnblogs.com/grandyang/p/10952459.html
http://blog.jerkybible.com/2018/03/09/LeetCode-794-Valid-Tic-Tac-Toe-State/


783. Minimum Distance Between BST Nodes
题要经常刷，久了不练就容易卡，这道题很好的考察了二叉搜索树的性质，
左小右大，那么要求两个节点差的最小值，左子树的最右节点，和右子树的最左节点，
根节点和它们之间一定有一个最小的，一个个递归下去检查

*779. K-th Symbol in Grammar
居然用到了二叉树的结构，没想到，利用父节点和子节点的关系递归回去
https://www.cnblogs.com/grandyang/p/9027098.html


1410. HTML Entity Parser
挺神奇的一道题，stack标签，但不知道怎么做，replace简单粗暴，看了一下顶踩比例，不满意的挺多。。。

1381. Design a Stack With Increment Operation
简单题，stack的最后k个值加val，那从最后一个数开始数做判断，
还有一个更简单的解法，不用stack倒来倒去，用数组来表示栈，index记录栈的值区间
refer:
https://leetcode.jp/leetcode-1381-design-a-stack-with-increment-operation-%E8%A7%A3%E9%A2%98%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90/


118. Pascal's Triangle
简单题，递归解决

155. Min Stack
明明是一道简单题，之前被自己必须一个栈的思路局限住了，其实可以两个栈，一个正常的，一个专门记录每个元素对应的最小值

173. Binary Search Tree Iterator
其实是搜索二叉树的中序遍历左右互换，入栈是从大到小，出栈反过来
时间复杂度还可以优化

224. Basic Calculator
题目本身不难，就是比较琐碎，首先考虑括号内的计算，算出来一个结果加入栈中，最后一起合并计算，
然后就是考虑括号内可能为负数，考虑符号的问题，细节处理好

*341. Flatten Nested List Iterator
题目没看懂，其实不难，和stack也没什么关系
refer:
https://blog.csdn.net/fuxuemingzhu/article/details/79529982

*95. Unique Binary Search Trees II
思路想到了，实现还有点问题

*641. Design Circular Deque 
直觉不难，但是写不出来，不知道怎么组织


933. Number of Recent Calls
简单题，把队列排在前面的不符合要求的元素poll掉就好了

*787. Cheapest Flights Within K Stops
应该是不难，不知道为什么本地运行结果和leetcode不一样
其他解法Bellman Ford有待了解
refer:
https://github.com/cherryljr/LeetCode/blob/master/Cheapest%20Flights%20Within%20K%20Stops.java
https://www.acwing.com/solution/LeetCode/content/634/

*1054. Distant Barcodes
手生了，知道是分组的思想，但是怎么实现，怎么也写不出来
refer:
https://leetcode.jp/leetcode-1054-distant-barcodes-%E8%A7%A3%E9%A2%98%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90/


*1439. Find the Kth Smallest Sum of a Matrix With Sorted Rows
排列组合，把所有可能放进去
refer：
https://leetcode.jp/leetcode-1439-find-the-kth-smallest-sum-of-a-matrix-with-sorted-rows-%E8%A7%A3%E9%A2%98%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90/

99. Recover Binary Search Tree
仔细理解题意，大意是一颗二叉搜索树，有两个位置交换了，导致不符合二叉搜索树的性质，现在要找到并恢复
那肯定是两个点不符合要求，根据二叉搜索树的性质，中序遍历是有序的，那么这个两个交换的节点肯定导致无序，
那就中序遍历，把结果存到一个list，再分别从前往后，从后往前检查，碰到的第一个不符合要求的点就是交换了的点

104. Maximum Depth of Binary Tree
简单题，递归调用好了

*450. Delete Node in a BST
同样是递归，一样的想法，不知道错在哪里
https://leetcode.com/problems/delete-node-in-a-bst/discuss/606590/Java-succinct-recursive-solution

*508. Most Frequent Subtree Sum
求和也递归好了，但是统计sum频率没想好怎么样比较快，
参考博主在递归的过程中用map记录sum的频率，淘汰小的，而不是等到最后筛选，这算是一个优化
refer:
https://www.cnblogs.com/grandyang/p/6481682.html

*33. Search in Rotated Sorted Array
又卡住了，问题在于确定有序区间，确定之后再判断，target可能落在哪边，确定的一面就可以就可以确定另一面

*275. H-Index II
这道题理解了题意应该挺简单的，到底是left<right还是left<=right要想清楚

1351. Count Negative Numbers in a Sorted Matrix
简单题，把二维拆成一维，每个都二分查找，注意元素会有相同的情况

1337. The K Weakest Rows in a Matrix
简单题，关键在于比较器，按数组的和排序即可

*1292. Maximum Side Length of a Square with Sum Less than or Equal to Threshold
没想出来，对于这个square的含义不理解，到底是正方形还是长方形，每个值是边长吗？还是说几个点就可以

*1283. Find the Smallest Divisor Given a Threshold
题意没读懂，大概是取商，有余数向上取整
refer:
https://www.cnblogs.com/wentiliangkaihua/p/12065983.html

*1201. Ugly Number III
和最小公倍数，最大公约数有关

*1095. Find in Mountain Array
还差一点点

**327. Count of Range Sum
思路混乱，不知道怎么缩小范围

*354. Russian Doll Envelopes
俄罗斯套娃，最长子序列一维到二维
https://blog.csdn.net/liuchonge/article/details/78404561

852. Peak Index in a Mountain Array
别管左边还是右边，就看mid处于左边上升区间还是右边下降区间

1391. Check if There is a Valid Path in a Grid
分情况讨论，深度优先

*1377. Frog Position After T Seconds
不知道为什么不对，就是从1出发无向图，深度优先搜索

*1376. Time Needed to Inform All Employees
没看懂manager之间的关系

2020/05/11
*1339. Maximum Product of Splitted Binary Tree
挺简单的题，没想清楚对应关系，总归是树砍成两半，那就每个节点都拆，除了叶子结点，
总和减去一个子树的和再乘以另外一个子树的和，就行了
refer:
http://www.noteanddata.com/leetcode-1339-Maximum-Product-of-Splitted-Binary-Tree-java-solution-note-2.html

*1319. Number of Operations to Make Network Connected
两种解法，一种是并查集，另外一种是广度优先？电缆数和节点的关系知道，但是怎么看够不够，就不清楚了
refer:
http://www.noteanddata.com/leetcode-1319-Number-of-Operations-to-Make-Network-Connected-java-solution-note.html
https://www.acwing.com/solution/LeetCode/content/7509/

*1254. Number of Closed Islands
题目不难，但是深度优先搜索的套路已经忘记了
染色标记
refer:
https://leetcode.jp/leetcode-1254-number-of-closed-islands-%E8%A7%A3%E9%A2%98%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90/

*542. 01 Matrix
这道题BFS,从0出发能到达的点，还有就是二次扫描，自己想法类似于二次扫描，但是不会实现
refer:
https://www.cnblogs.com/grandyang/p/6602288.html

**546. Remove Boxes
题目没看懂，其实类似于消消乐得分,解法也不好懂
refer:
https://blog.csdn.net/magicbean2/article/details/78866298

733. Flood Fill
简单题，还是DFS的基本套路


690. Employee Importance
ToDo
注意结果作为实参传递没变，搞不清楚为什么，难道是因为结果是原始类型？？？

*886. Possible Bipartition
思路是一样的，为什么没能实现呢？错在节点遍历这里，标准流程，构建图，节点遍历检查，是否满足条件
两种解法，深度优先DFS,并查集
https://www.cnblogs.com/grandyang/p/10317141.html
http://www.noteanddata.com/leetcode-886-Possible-Bipartition-java-solution-note.html

721. Accounts Merge
不刷题手生，一个邮箱对应一个用户，一个用户有很多邮箱，图的问题，
解法一：并查集，每个邮箱的根是用户名，根相同的即为一个账户
解法二：BFS，邮箱和账户之间的映射
https://www.cnblogs.com/grandyang/p/7829169.html

20200710
638. Shopping Offers
不刷题手生+1，购物券买东西，求最低价
refer:
https://blog.csdn.net/Jacky_chenjp/article/details/75329090

542. 01 Matrix
广度优先更好，利用矩阵只有0，1值的特征


1448. Count Good Nodes in Binary Tree
下次消灭，递归没实现

    3
  1   4
3   1   5


403. Frog Jump
关键在于理解，上一步跳k步远，下一步k,k-1,k+1,所以怎么到达的这个位置很重要，把每个位置可能跳的距离记录下来，遍历判断
refer:
http://www.noteanddata.com/leetcode-403-Frog-Jump-java-solution-note.html


*464. Can I Win
记忆状态,没搞明白状态转移方程式
http://www.noteanddata.com/leetcode-464-Can-I-Win-java-solution-note.html
https://www.jianshu.com/p/b7db270b7577


235. Lowest Common Ancestor of a Binary Search Tree
寻找最近的公共祖先节点，根据二叉搜索树的特点，左小右大，那么祖先节点的值大小肯定在这两个节点之间，从根节点遍历，只要一个节点的值满足条件必然是最近的，
不然一边倒，要么都大，要么都小，根据大小决定向左向右的遍历方向


572. Subtree of Another Tree
注意审题，二叉树不是二叉搜索树，节点值甚至有重复的情况，所以当两个节点的值相同时，如果判断一个是另一个的子树，那它们之间有一部分一定完全相同，当前节点的树是否相同，或者是左右子节点的子树


*538. Convert BST to Greater Tree
这道题的大意是把一个节点的值更新为包括自己在内的右子树的和，大致思路其实就是中序遍历倒过来，右中左，从右边开始更新，每个更新的节点等于它本身的值加上上次更新的节点的新值，中序遍历有点忘了，写成了死循环，要点就是，一直向右遍历直到为空，弹出新节点，遍历这个新节点的左子树，即让当前节点等于它的左子节点

*543. Diameter of Binary Tree
简单题，思路是对的，实现写的太复杂了，其实没搞清楚直径的概念，在这里和每个节点本身的值无关，只和高度有关

404. Sum of Left Leaves
简单题，首先明确叶子节点的概念，就是到头了，其次所有的叶子节点之和，其实就是中序遍历，每遍历到一个左子节点判断是不是叶子节点，是就加上去

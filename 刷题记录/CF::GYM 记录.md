## gym103371J. Periodic Ruler

[link](https://codeforces.com/gym/103371/problem/J)

先排除不能作为周期的正整数，也就是所有不同数对的坐标之差的所有约数。

然后再找不能满足是最小正周期的正整数，这样的数 $k$ 一定是 $\le n$ 的。因为如果 $k> n$ 把其他所有点映射到 $[0,k)$ 中，至少有一个空位，可以放一个 unique 的数。

然后怎么暴力怎么来。

[submission(3)](https://codeforces.com/gym/103371/submission/142551700)

## gym102268J. Jealous Split

[link](https://codeforces.com/gym/102268/problem/J)

**做法 1**

假设划分的相邻两段 $[l,m],[m+1,r]$ 和为 $A,B$，假设 $A> B$，如果 $A-B> a_m$，可以调整至 $A-a_m,B+a_m$ 更优，直至合法。

上述过程导致划分的平方和一定变小（次数 $>1$ 就行），最小化平方和的方案一定合法。

那么 wqs 二分解决。构造方案的话，可以二分完 $\Delta$ 后，尽量少划分、尽量多划分分别 DP 一遍，然后从后往前枚举点，取当前段数在点的段数范围内的作为分界点。

[submission(3)](https://codeforces.com/gym/102268/submission/142790657)

**做法 2**

惊人的洞察力。

定义一个 $x$ 划分为，每次贪心取最小一段且和 $\ge x$ 进行划分。

二分最大的 $k=x$ 使得 $k$ 划分 $\ge m$ 段。

然后倒着进行 $k+1$ 划分。

两者分界点一定有若干重合点，并且不存在某个 $k+1$ 划分的段包含某个 $k$ 划分的段。[正确性证明](https://www.cnblogs.com/flyfeather6/p/12034455.html)。

一定可以找到一个重合点，满足左边 $k$ 划分和右边 $k+1$ 划分拼起来总共是 $m$ 段。

## gym103119B. Boring Problem

[link](https://codeforces.com/gym/103119/problem/B)

对 $\{T_i\}$ 建出 AC 自动机，DP $f_u$ 表示 $u$ 节点到达某个终止节点的期望步数，

$$
f_u=1+\sum_{c\in\Sigma}p_cf_{\mathrm{ch}(u,c)}
$$

高斯消元可以做大 $\mathcal O((nm)^3)$。

考虑主元法，将 AC 自动机的根设为主元，对于 $u$，

- 如果 $u$ 有 $1$ 个 trie 树上的儿子 $v$，那么 $f_v$ 可以用 $f_u$ 和 $u$ 的其他转移后继推出；
- 如果 $u$ 有多于 $1$ 个 trie 树上的儿子，不妨把这些儿子也设为主元。

由于 $n$ 个串 trie 树的分叉点个数是 $\mathcal O(n)$ 的，所以主元个数也是 $\mathcal O(n)$ 的。

然后用所有分叉点和叶子节点的列出方程，这样方程数恰好是主元个数，高斯消元即可，$\mathcal O(n^3)$。

[submission(1)](https://codeforces.com/gym/103119/submission/143047350)

## gym103119I. Nim Cheater

[link](https://codeforces.com/gym/103119/problem/I)

可以 DP $f(i,j)$ 表示前 $i$ 堆石子使得异或和为 $j$ 的最小代价，时间空间复杂度都为 $\mathcal O(na)$，空间不行。

将询问离线建出树形结构，我们发现为了回溯，需要记录当前点所有祖先的状态。但是如果当前点是父亲最后一个访问的儿子，则不需要留下父亲的状态。

那么重链剖分，重儿子最后访问，需要记录的祖先个数就是 $\mathcal O(\log n)$ 个了，空间复杂度 $\mathcal O(a\log n)$。

[submission(2)](https://codeforces.com/gym/103119/submission/143049689)

## gym103202J. Descent of Dragons 

[link](https://codeforces.com/gym/103202/problem/J)

记录 $f(i,x)$ 表示 $i$ 位置是否 $\ge x$。

每个权值开一个线段树，记录包含的下标集合。那么每次修改操作就是 $x$ 线段树到 $x+1$ 线段树的区间复制，用可持久化线段树解决。

查询可以二分。复杂度 $\mathcal O(q\log q\log n)$。

注意复制 $v\to u$ 时，$u$ 节点原来的信息不能被覆盖。

[submission(1)](https://codeforces.com/gym/103202/submission/143052650)

## gym103202M. United in Stormwind

[link](https://codeforces.com/gym/103202/problem/M)

每个人的答案用二进制数表示，那么相同的一对就是异或值为 $0$ 的一对。

FWT 做 xor 卷积算出异或值为 $k$ 的对数，然后考虑 $k$ 的贡献，就是再做一下超集和。

[submission(1)](https://codeforces.com/gym/103202/submission/143071670)

## gym102992J. Just Another Game of Stones

[link](https://codeforces.com/gym/102992/problem/J)

每次查询时，设 $s$ 为区间 $[l,r]$ 和 $x$ 的异或和，那么先手获胜的条件为操作某一个数 $k\to k-\Delta$，使得 $s\oplus k\oplus (k-\Delta)=0$，简单讨论一下就是 $k$ 需要包含 $\mathrm{highbit}(s)$ 这一位。

修改操作使用 Segment Tree Beats，同时维护区间异或和、每一位包含这一位的个数。

[submission(1)](https://codeforces.com/gym/102992/submission/143089157)

## gym103081J. Daisy's Mazes

[link](https://codeforces.com/gym/103081/problem/J)

发现经过一段括号序列是没有花费的（若每一步都合法）。

加入 $n-1$ 个虚点，和起点排在一起，第 $i$ 个向第 $i-1$ 个连所有颜色的边，虚点到起点的路径表示初始栈；终点向自身连所有颜色的边，消去剩余栈。

此时问题转化为以某个虚点为起点，是否能经过一段括号序列到达终点。

DP 设 $f(c,u,v)$ 表示当前栈顶为 $c$ 时，$u$ 是否能到达 $v$。转移时考虑拼接两个括号序列、在外面嵌套一层。

因为顺序不好确定，可以 DFS 来递推。

[submission(1)](https://codeforces.com/gym/103081/submission/143510075)

## gym102984J. Setting Maps

[link](https://codeforces.com/gym/102984/problem/J)

考虑网络流做法。设 $d_u,e_u$ 表示 $u$ 点（不包含 / 包含）之前的所有路径上最少关键点数。有如下限制：

- $d_u\le e_u\le d_u+1$，若 $e_u=d_u+1$ 则有 $c_u$ 的代价；
- 每条边 $(u,v)$，$e_u\ge d_v$；

转化为最小割模型，将每个变量拆成 $k+1$ 个点，用 $(i,i+1,0)$ 边连起来，割代表选。

对于每个 $x\le y$ 的限制，连边 $(x,y,+\infty)$（切糕）。

[submission(2)](https://codeforces.com/gym/102984/submission/143584478)

## gym103470E. Paimon Segment Tree

[link](https://codeforces.com/gym/103470/problem/E)

先询问离线差分，否则将下面的操作改成可持久化会 MLE。

将每次修改拆成 $([0,l-1],0),([l,r],x),([r+1,n],x)$ 三个修改，那么用每个数记录 $[1,a_i,a_i^2,\sum a_i^2]$ 即可用矩阵转移。用线段树维护。

$4\times 4$ 的矩阵有点大，但是上三角矩阵相乘还是上三角矩阵，剪枝后常数 $\frac 16$。

[submission(5)](https://codeforces.com/gym/103470/submission/143619181)

## gym103447L. Karshilov's Matching Problem

[link](https://codeforces.com/gym/103447/problem/L)

用栈取维护当前串的每个同色连续段，一段同色连续段的价值可以在 AC 自动机上倍增来求。

[submission(1)](https://codeforces.com/gym/103447/submission/143627204)



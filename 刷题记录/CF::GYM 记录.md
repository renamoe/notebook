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



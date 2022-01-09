## ARC125D - Unique Subsequence

[link](https://atcoder.jp/contests/arc125/tasks/arc125_d)

DP 设 $f(i)$ 表示 $i$ 结尾的合法子序列个数。每个数字只在最后一次出现时的 $f$ 值是有效的。

发现对于子序列 $a_{p_1}\dots a_{p_k}$，任意两个相邻的数 $a_{p_i}$ 和 $a_{p_{i+1}}$ 之间不能存在等于 $a_{p_i}$ 或 $a_{p_{i+1}}$ 的数，否则非法。

那么转移时，强制每个数 $a_i$ 从上一次出现的位置 $\mathrm{last}(a_i)\dots i-1$ 转移，并且任何时刻每个数字只在最后一次出现的位置保留 $f$ 值，可以用树状数组维护。

[submission(0)](https://atcoder.jp/contests/arc125/submissions/25514677)

## ARC015D - Let's Play Nim

[link](https://atcoder.jp/contests/arc105/tasks/arc105_d)

考虑石子堆的异或和。$n$ 的奇偶性关系到最后做 nim 游戏的先后手，分类讨论：

- $n$ 为偶数，先手加入石子堆时要尽量让异或和不为 $0$。如果石子堆可以两两配对相等的话，后手就可以复刻先手的动作从而先手必败。否则先手可以一直掌握最大的石子堆：每次挑最大的石子堆加入同一盘子，可以保证该盘严格大于其它石子堆和，异或和不为 $0$。
- $n$ 为奇数，先手要尽量让异或和为 $0$。但是后手有同样的掌握最大石子堆的策略，先手必败。

## ARC105E - Keep Graph Disconnected

[link](https://atcoder.jp/contests/arc105/tasks/arc105_e)

终止局面一定是 $n$ 个点分为两个连通块 $a,b$，总步数就是 $\frac{n\times (n-1)}{2}-a\times b-m$。

总步数的奇偶性决定先后手的胜负。因为 $a+b=n$，我们讨论 $n$ 的奇偶性：

- $n$ 为奇数：$a\times b$ 一定是偶数，总步数奇偶性直接确定。
- $n$ 为偶数：考虑操作过程对 $a\times b$ 奇偶性的影响，设一开始 $1,n$ 所在连通块大小分别为 $x,y$，每次操作可以通过将奇数大小的连通块于其中之一连接，来改变奇偶性。
  - $x,y$ 奇偶性相同：可以推出奇数大小连通块数为偶数个，操纵奇数大小连通块的策略会两两抵消，奇偶性不会改变；
  - $x,y$ 奇偶性不同：可以推出奇数大小连通块数为奇数个，先手可以第一步通过操纵奇数大小连通块，将 $a\times b$ 变成奇数或者偶数，后续同上，先手必胜。

[submission(1)](https://atcoder.jp/contests/arc105/submissions/25880016)


## ARC104E - Random LIS

[link](https://atcoder.jp/contests/arc104/tasks/arc104_e)

求 LIS 我们需要知道数之间的相对大小关系，$N$ 很小所以考虑直接枚举所有 $N!$ 个情况。

枚举排列 $p_1\dots p_N$ 表示 $a_{p_1}(<\mathrm{or}\le)a_{p_2}(<\mathrm{or}\le)a_{p_3}\dots a_{p_N}$。由于这里 LIS 是严格递增的，我们枚举的排列是按双关键字（权值、下标）排序的：如果 $p_i<p_{i+1}$，那么要让 $a_{p_i}$ 能贡献到 $a_{p_{i+1}}$，一定是 $a_{p_i}< a_{p_{i+1}}$；否则 $a_{p_i}\le a_{p_{i+1}}$。

将所有数按 $p$ 从小到大排列。为了方便我们将 $<$ 统一成 $\le$，也就是将 $<$ 后面的数取值范围减小 $1$。然后将取值范围做后缀 $\min$，记为 $\{h_i\}$，现在问题转化为求满足 $1\le a_i\le h_i$ 且 $a_i\le a_{i+1}$ 的序列 $\{a_i\}$ 方案数。

对于 $\le$ 的关系可以想到格路计数（网格图中每次向右或向上走一步，向右走一步代表结尾填一个数），$h_i$ 的限制可以容斥处理。设 $f_i$ 表示网格图中前 $i$ 条竖线合法方案数，然后去枚举第一次超出限制的位置进行容斥，

$$
f_i\gets {h_i-1+i-1\choose i-1}-\sum_{j < i}{h_i-h_j-1+i-j\choose i-j}f_j
$$

组合数均为 ${x+y\choose y}$ 的形式，可以 $\mathcal O(y)$ 计算。总复杂度 $\mathcal O(N!N^3)$。

[submission(4)](https://atcoder.jp/contests/arc104/submissions/26060672)

## ARC066B - Xor Sum

[link](https://atcoder.jp/contests/abc050/tasks/arc066_b)

观察性质：因为异或是不进位加法，所以 $a+b=(a\operatorname{and} b)\times 2+(a\operatorname{xor}b)$，即 $u\le v$。我们对每个 $v$ 去统计可配对的 $u$。

可以发现 $u,v$ 唯一对应一对 $a,b$ $(a < b)$。逐位考虑 $a,b$，最低位有 $(0,0),(0,1),(1,1)$ 三种情况，我们去掉其贡献，那么可以递归的考虑剩余位，这样只递归 $\log$ 次。

具体地，我们可以列出转移，

$$
f(k)\gets \begin{cases}
f(\frac k2)+f(\frac{k-2}{2})&2\mid k\\
f(\frac{k-1}{2})&2\not\mid k
\end{cases}
$$

然后我们对 $f$ 做前缀和，推式子可以得到非常简洁的式子：

$$
s(k)=s(\lfloor\frac{k}{2}\rfloor)+s(\lfloor\frac{k-1}{2}\rfloor)+s(\lfloor\frac{k-2}{2}\rfloor)
$$


## ARC103D - Robot Arms

[link](https://atcoder.jp/contests/arc103/tasks/arc103_b)

有解的条件是 $x+y$ 奇偶性相同，为 $\sum d_i$ 的奇偶性。

根据 $m$ 的限制应该想到二进制拆分。

$1,2,4\dots$ 能够覆盖的范围，再网格图上表示为一层层菱形覆盖的所有 $x\equiv y\pmod 2$ 的点。根据奇偶性可能需要加一个 $1$ 偏移一下。构造方式就是 $d_i$ 从大到小每次选择距离绝对值较大的移位移动，能够覆盖所有可到达的点。

[submission(3)](https://atcoder.jp/contests/arc103/submissions/27017414)

## ARC103E - Tr/ee

[link](https://atcoder.jp/contests/arc103/tasks/arc103_c)

首先注意到一定要 $s_1=1,s_n=0$ 并且 $s_i=s_{n-i}$ 才合法。

构造就是一层一层的菊花，因为 $1$ 大小的连通块是一定存在的；所以从大到小枚举，存在就将后续的点放入该点子树，否则挂在上一层的父亲上。

[submission(2)](https://atcoder.jp/contests/arc103/submissions/27019058)

## ARC103F - Distance Sums

[link](https://atcoder.jp/contests/arc103/tasks/arc103_d)

首先 $d$ 最大的是叶子，最小的是重心。

以重心为根，产生的性质是 $d_{\mathrm{fa}_u} < d_{u}$。

那么可以从叶子往根递推，$u$ 的父亲的权值为 $d_u-(n-\mathrm{size}_u)+\mathrm{size}_u$。

最后需要再换根 DP check 一下是否合法，因为此时只保证的相对大小关系，比如 $d=\{1,2\}$ 的情况就不合法。

[submission(0)](https://atcoder.jp/contests/arc103/submissions/27020067)

## ARC102D - All Your Paths are Different Lengths

[link](https://atcoder.jp/contests/arc102/tasks/arc102_b)

二进制拆分。

每个点 $i$ 向 $i+1$ 连边 $0,2^{20-i-1}$，代表从 $i$ 点开始的所有路径范围为 $[0,2^{20-i})$。点数卡的紧，需要特判一下 $1,2$ 之间是否需要连。

然后二进制拆分 $L$，从 $1$ 点向对应点连边。

[submission(0)](https://atcoder.jp/contests/arc102/submissions/27021723)


## ABC225F - String Cards

[link](https://atcoder.jp/contests/abc225/tasks/abc225_f)

首先要排序，使得我们选取任意一个子集时，按这个顺序一定是字典序最小的。

直接按字典序排序是不对的，反例：$\texttt{b},\texttt{ba}$ 选两个。

正确的排序方式是 $A+B < B+A$ 才能 $A$ 在 $B$ 之前，那么一定可以通过交换相邻项得到。将字符串看作 $26$ 进制数，推一下相当于比较 $\displaystyle \frac{a}{26^{|A|}-1}<\frac{b}{26^{|B|}-1}$，只和自身有关，所以这么排是没有问题的。

然后直接取前 $k$ 小也是不对的，反例：$\texttt{b},\texttt{ba}$ 选一个。

应该 DP，设 $f(i,j)$ 表示以 $i$ 开头选 $j$ 个字符串的最小答案，倒序转移。

正着 DP 是不对的，因为字典序前面的起决定性作用。或者可以想想直观的记忆化搜索写法，从后到前转移才是正确的划分出了子问题。

代码咕。

## AGC036F - Square Constraints

[link](https://atcoder.jp/contests/agc036/tasks/agc036_f)

首先观察，是在 $(0,0),(2n-1,2n-1)$ 的矩形中，画半径 $n,2n$ 的圆，令两圆之间的整点为 $1$，其余为 $0$。求矩形格点形成矩阵的积和式。

![嫖张图](https://s4.ax1x.com/2021/12/20/TnhsY9.png)

先考虑没有小圆的限制，那么从上到下，一行一行地放点，设第 $i$ 行可放位置数为 $R_i$，答案为 $\prod_i(R_i-i+1)$。

对于小圆，考虑容斥，下方有 $n$ 行受到小圆限制，枚举其中 $k$ 行放在小圆内进行容斥。

要计算这一部分的方案数，每放一个点需要知道其限制 $R_i$ 或 $r_i$ 在所有行中的排名。

上面 $n$ 行称为 $A$ 类，下面 $n$ 行称为 $B$ 类。$A$ 类按 $R_i$ 为关键字，$B$ 类按 $r_i$ 为关键字，排序。

这样：

- $A$ 类的排名，就是它前面的 $A$ 类个数和 $B$ 类选择 $r_i$ 的个数；
- $B$ 类选择 $r_i$ 时，排名也是它前面的 $A$ 类个数和 $B$ 类选择 $r_i$ 的个数；
- $B$ 类选择 $R_i$ 时，排名是所有 $A$ 类个数、$B$ 类选择 $r_i$ 个数、和它前面 $B$ 类选择 $R_i$ 的个数。

那么 DP 设 $f_k(i,j)$ 表示前 $i$ 行有 $j$ 个 $B$ 类选择 $r_i$，的方案数。做 $k$ 遍 DP 是必要的，因为计算 $B$ 类选择 $R_i$ 的排名需要确定 $k$。

复杂度 $\mathcal O(n^3)$。

[submission](https://atcoder.jp/contests/agc036/submissions/28033373)

## ARC102E - Stop. Otherwise...

[link](https://atcoder.jp/contests/arc102/tasks/arc102_c)

对于权值 $i$，如果 $i<x$，$i$ 和 $x-i$ 只能允许其中一个被选；特别地，$i=x-i$ 时，这个值至多选一个；其余的值随意选。

设第一类权值对有 $a$ 个，随意选的权值有 $b$ 个。

列出式子，

$$
\sum_{i=0}^a\binom{a}{i}2^i\sum_{j=i}^n\binom{j-1}{i-1}\left(\binom{n-j+b-1}{b-1}+\binom{n-1-j+b-1}{b-1}\right),
$$

可以 $\mathcal O(n^3)$。

改一改，

$$
\sum_{j=0}^n\left(\binom{n-j+b-1}{b-1}+\binom{n-1-j+b-1}{b-1}\right)(j-1)!\sum_{i=0}^{\min(a,j)}\binom{a}{i}2^i\frac{1}{(i-1)}\frac{1}{!(j-i)!}
$$

把 T2 写的 NTT 粘过来就 $\mathcal O(n^2\log n)$ 了。

幸好给的 $2000$，简单卡卡常就过了。

[submission](https://atcoder.jp/contests/arc102/submissions/28029511)

下面记录一个更优秀的做法：

- 考虑二选一权值对的 OGF为 $1+2x+2x^2+\dots$；
- 至多选一次的权值的 OGF 为 $1+x$；
- 随意选的权值的 OGF 为 $1+x+x^2+\dots$。

最后分配 $n$ 个骰子的权值，答案为

$$
[x^n]\left(\frac{1+x}{1-x}\right)^a\cdot (1+x)^{[2|x]}\cdot \left(\frac{1}{1-x}\right)^b
$$

$$
[x^n]\frac{(1+x)^A}{(1-x)^B}
$$

我们知道 $[x^i](1+x)^A=\dbinom{A}{i}$，$[x^i]\dfrac{1}{(1-x)^B}=\dbinom{i+B-1}{B-1}$，每次可以 $\mathcal O(n)$ 卷积得到单点答案。总复杂度 $\mathcal O(nK)$。

[submission](https://atcoder.jp/contests/arc102/submissions/28030809)

## AGC028D - Chords

[link](https://atcoder.jp/contests/agc028/tasks/agc028_d)

计数所有方案的连通块个数，有两种方式：

- 一种是同时维护所有方案连通块个数的 $0$ 次和和 $1$ 次和，问题在于 $0$ 次和（方案数）并不好计算（我只 yy 出了 $\mathcal O(n^4)$ 做法，并且难以处理给出的定边）。
- 另一种方式是有意地重复计算每个方案，在每个连通块处统计一次所在方案。或者理解为计算贡献。

从 $1,2n$ 处断开，一个方案的所有连通块，只存在并列或包含的关系。一个连通块的贡献，在连通块点集的编号最小点和编号最大点组成点对 $(l,r)$ 处统计。

记 $f(l,r)$ 表示只考虑区间 $[l,r]$ 内所有点，$l,r$ 连通的方案数。$l,r$ 连通的限制，用容斥处理，枚举 $l$ 所在连通块的最大编号，$f(l,r)$ 可以递归地表示。

那么 $f(l,r)$ 乘上 $[l,r]$ 以外随意连的方案数，就是包含连通块 $(l,r)$ 的方案数。

复杂度 $\mathcal O(n^3)$。

将来的自己没看懂的话，想一想方案、连通块、点对之间的映射关系。

[submission(0)](https://atcoder.jp/contests/agc028/submissions/28077775)

## ARC101E - Ribbons on Tree

[link](https://atcoder.jp/contests/arc101/tasks/arc101_c)

容斥，钦定一个边集不被染色，那么树会分裂成若干小连通块，每个小连通块随意匹配。

每个不被染色的边贡献 $-1$ 的容斥系数，树形 DP，记 $f(u,i)$ 表示 $u$ 子树中，$u$ 所在连通块大小为 $i$，$u$ 所在连通块以外的贡献。

转移就是树上背包的合并，同时考虑一下是否形成新的连通块。

复杂度 $\mathcal O(n^2)$。

[submission(1)](https://atcoder.jp/contests/arc101/submissions/28075967)


## AGC027E. ABBreviate

[link](https://atcoder.jp/contests/agc027/tasks/agc027_e)

令 $\texttt a\to 1,\texttt b\to 2$，$f(S)$ 为字符串 $S$ 各字符之和 $\bmod 3$。

字符串串 $S$ 能够变成字符 $c$ 的条件为两者之一：

- $S=c$；
- $f(S)=f(c)$ 并且 $S$ 中存在相邻相同的一对字符。

题目转化为，统计字符串 $T$ 的数量，满足 $S$ 划分成 $|T|$ 部分后，每个部分能够变成 $T$ 中的对应字符。

从左到右贪心地划分，每次取尽量短的合法子段，记为 $A_{1\dots |T|}$。最后会剩下一部分，记为 $R$。

该划分合法地条件是 $f(R)=0$，证明：

- $A_{|T|}+R$ 中存在相邻相同的一对字符，则可以并入 $A_{|T|}$；
- 否则 $A_{|T|}+R$ 一定形如 $\texttt{ababababa\dots}$，将 $A_{|T|}$ 改为 $R$ 最后一个字符，归纳为剩余部分 $R'$ 与 $A_{|T|-1}$ 的子问题。

那么可以 DP，额外记录 $\mathrm{nxt}_{\texttt a/\texttt b}(i)$ 表示 $i$ 开头最小的能够变成 $\texttt a/\texttt b$ 的字段后面一位是谁。

注意特判整串无法操作的情况。

[submission(0)](https://atcoder.jp/contests/agc027/submissions/28364375)

## AGC010D. Decrementing

[link](https://atcoder.jp/contests/agc010/tasks/agc010_d)

终止状态为全 $1$，那么关注 $\sum_i(a_i-1)$ 的奇偶性。

- 如果存在 $1$，后续回合 $\gcd$ 都为 $1$，胜负取决于 $\sum_i(a_i-1)$ 的奇偶性。
- 如果有奇数个偶数，先手一定是操作一个偶数，无论后手如何应对，先手都能保持 $\sum_i(a_i-1)$ 为偶数。先手必胜。
- 如果有偶数个偶数：
  - 如果有大于 $1$ 个奇数，那么无论如何操作，后手都是必胜态。
  - 如果有 $1$ 个奇数，先手只能操作这个奇数，$\gcd$ 变为偶数，除 $\gcd$ 会改变很多数的奇偶性，递归下去处理（不超过 $\log$ 次）。
  - 由于每操作一轮后所有数互质，不可能全是偶数。

[submission(1)](https://atcoder.jp/contests/agc010/submissions/28369369)

## AGC024E. Sequence Growing Hard

[link](https://atcoder.jp/contests/agc024/tasks/agc024_e)

字典序的限制可以描述为，每次在一个数前面插入一个严格比它大的数。

加入一个虚点表示最开始空序列里的数。给每个点 $\mathrm{id}_i,\mathrm{val}_i$ 表示插入的顺序、权值。每次在一个数前面插入一个严格比它大的数，可以描述为树形结构，即插入一个编号最大的点到某一个点下面。可以发现这种有根树和原序列的序列构成双射。

考虑 DP，设 $f(n,x)$ 表示 $n$ 个点的有根树，根（$1$ 号点）的权值为 $x$ 的方案数。$2$ 号点一定是根直接的儿子，将树划分成两部分，递归然后分配标号：

$$
f(n,x)\gets \sum_{i=1}^{n-1}\left(\sum_{y> x}f(i,y)\right)\times f(n-i,x)\times\binom{n-2}{i-1}
$$

后缀和优化即可 $\mathcal O(n^2K)$。

[submission(0)](https://atcoder.jp/contests/agc024/submissions/28373255)


## AGC023E. Inversions

[link](https://atcoder.jp/contests/agc023/tasks/agc023_e)

考虑每个点对 $(i,j)$ 的贡献。

如果 $a_i=a_j$，发现 $(i,j)$ 构成逆序对的方案数是总方案数的一半。

计算总方案数，可以从大往小放数。设 $\mathrm{cnt}(k)$ 表示 $\left(\sum_i[a_i\ge k]\right)-(n-k)$，那么从方案数就是 $S=\prod_{i=1}^n\mathrm{cnt}(i)$。

如果 $a_i< a_j$，不妨令 $a_j\gets a_i$，贡献为修改后的总方案数的一半。这样的修改产生的影响是，$\forall k\in [i+1,j],\mathrm{cnt}(k)\gets \mathrm{cnt}(k)-1$。设 $\displaystyle D(k)=\prod_{i=1}^k\frac{\mathrm{cnt}(k)-1}{\mathrm{cnt}(k)}$，修改后的方案数可以表示为 $S\times \dfrac{D(j)}{D(i)}$。

那么可以和二维偏序一样用树状数组维护。需要注意的是 $\mathrm{cnt}(k)-1$ 可能为 $0$，可以记录乘积中 $0$ 的个数，由于 $0$ 的个数在前缀积中是单调的，$\frac{D(j)}{D(i)}\neq 0$ 当且仅当 $D(i),D(j)$ 包含 $0$ 的个数相同，每次查询一个区间即可。

如果 $a_i>a_j$，可以用总方案数减去构成顺序对的方案数，就和上面一样了。

[submission(0)](https://atcoder.jp/contests/agc023/submissions/28425738)


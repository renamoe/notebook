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





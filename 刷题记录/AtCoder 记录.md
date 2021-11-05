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





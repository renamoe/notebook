
## BZOJ#4350. 括号序列再战猪猪侠

[link](https://hydro.ac/d/bzoj/p/4350)

按给出的偏序关系建图，有环无解。

然后数据范围很小，考虑区间 DP。过程共需要知道 $[l_1,r_1]$ 的左括号对应的右括号是否可以在 $[l_2,r_2]$ 的左括号对应的右括号之前。设 $A(i,j)$ 表示 $i$ 的右括号是否**不能**在 $j$ 的右括号之前，每次查询的就是一个子矩形内是否全为 $0$，预处理二维前缀和。

[code(1)](https://gitee.com/renamoe/pastebin/blob/master/BZOJ4350.cpp)

## 51Nod#1327. 棋盘游戏

[link](https://vjudge.net/problem/51Nod-1327)

考虑如果只有左边的限制，那么我们可以设 $f(i,j)$ 表示前 $i$ 列，有 $j$ 列没有放的方案数。每次到达一些边界的时候我们都要强行满足它们，取出前面的一些空列，因为有序所以乘一个阶乘。

如果只有右边，那么我们可以设 $f(i,k)$ 表示做到第 $i$ 列，有 $k$ 行没有满足的方案数。每次到达一些边界 $k$ 就可以增加。

然后两个 DP 合在一起。$\mathcal O(m^2n)$。

[code(3)](https://gitee.com/renamoe/pastebin/blob/master/51Nod1327.cpp)

## HDU#6416. Rikka with Seam

[link](https://vjudge.net/problem/HDU-6416)

一行内，一个同色的连续段删去哪一个都是一样的。

对于结果相同的所有方案，考虑在字典序最小处计算。因为 $k$ 的限制，一个连续段的不同位置也会有不同的贡献。

逐行 DP，设 $f(i,j)$ 表示 $(i,j)$ 结尾的方案数；$g(i,j)$ 表示 $f(i,j)$ 去掉 $f(i,j-1)$ 已经计算过的的方案数。

转移的时候 $i-1$ 行的查询区间 $[j-k,j+k]$，$j-k$ 位置贡献的是 $f$，$j-k+1\dots j+k$ 贡献的是 $g$。

$f,g$ 转移时不同的地方在于，如果 $(i,j),(i,j-1)$ 颜色相同，$g$ 就只需要考虑 $(i-1,j+k)$ 的贡献。

HDU 死了，没处交。

## BZOJ#2169. 连边

设 $f(i,j)$ 表示连 $i$ 条边时奇点个数为 $j$ 的方案数，转移时讨论两奇点相连、一奇一偶相连、两偶点相连即可。

注意这样会造成重边，那么算出恰好有一条重边的方案数并减掉。

由于是有序地考虑每条边，每次还要除以 $i$。

$\mathcal O(nk)$。

[code(1)](https://gitee.com/renamoe/pastebin/blob/master/BZOJ2169.cpp)

## LOJ#2038. 「SHOI2015」超能粒子炮・改

[link](https://loj.ac/p/2038)

用 lucas 定理拆成递归形式：

$$
\begin{aligned}
f(n,k)&=\sum_{i=0}^k\binom{n}{i}\\
&=\sum_{i=0}^k\binom{\lfloor n/p\rfloor}{\lfloor i/p\rfloor}\binom{n\bmod p}{i\bmod p}\\
&=\sum_{i=0}^{\lfloor k/p\rfloor-1}\binom{\lfloor n/p\rfloor}{i}\sum_{j=0}^{p-1}\binom{n\bmod p}{j}+\binom{\lfloor n/p\rfloor}{\lfloor k/p\rfloor}\sum_{i=0}^{k\bmod p}\binom{n\bmod p}{i}\\
&=s(n\bmod p,p-1)\cdot f(\lfloor \frac{n}{p}\rfloor,\lfloor \frac{k}{p}\rfloor-1)+\binom{\lfloor n/p\rfloor}{\lfloor k/p\rfloor}\cdot s(n\bmod p,k\bmod p)
\end{aligned}
$$

$s(i,j)$ 为组合数行前缀和。$\dbinom{\lfloor n/p\rfloor}{\lfloor k/p\rfloor}$ 用 lucas 计算。

复杂度 $\mathcal O(p^2+T\log_p^2n)$。

[submission(2)](https://loj.ac/s/1323022)

## 51Nod#1248. 子序列之和

[link](https://vjudge.net/problem/51Nod-1248)

首先 $F$ 是个类似斐波那契的数列，其生成函数为 $F(x)=\dfrac{1-3x}{1-6x+x^2}$，解得通项为 $F_n=\dfrac{(3+2\sqrt 2)^n+(3-2\sqrt 2)^n}{2}$。这样我们要求的就是某个幂次之和了。

绝对值还是不好处理。观察到两个根 $(3+2\sqrt 2)\times (3-2\sqrt 2)=1$，也就是说 $F_n=\dfrac{r^n+r^{-n}}{2}$，$n$ 为正负的结果是一样的。

然后就是求 $\displaystyle \sum_{S\subseteq U}r^{\mathrm{sum}(S)-\mathrm{sum}(U\setminus S)}$，考虑每个数 $a_i$ 是否选，DP 一下。

[code(0)](https://gitee.com/renamoe/pastebin/blob/master/51Nod1248.cpp)


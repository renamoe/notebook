## UOJ#105. 【APIO2014】Beads and wires

[link](https://uoj.ac/problem/105)

一条蓝线连接连续三个点，直接 DP 发现并不对，反例：

![](https://s4.ax1x.com/2021/12/16/T9FpdO.png)

但是根据生成的过程，如果确定一个根，所有蓝线一定是 $u-\mathrm{fa}(u)-\mathrm{fa}(\mathrm{fa}(u))$ 的形态。

DP 设 $f(u,0/1)$ 表示 $u$ 是否为蓝线中点的最大价值。$f(u,1)$ 中某个儿子的贡献是不一样的，而且是最大值，换根 DP 时如果该儿子 $v$ 是最大值，那么去掉 $v$ 的贡献后应该由次大值顶替。

[submission(2)](https://uoj.ac/submission/520805)

## UOJ#290. 【ZJOI2017】仙人掌

[link](https://uoj.ac/problem/290)

不妨把所有环上的边删掉，剩下一个森林，不同联通块之间一定不能连边，否则就不是仙人掌了，那么把每棵树的方案数乘起来即是答案。

仙人掌中不属于任何一个环的边，不妨用一个重边覆盖，这样就可以转化为用若干边不相交的路径覆盖一棵树的方案数。

设 $g(u)$ 表示 $u$ 子树及其父亲边的方案数，

$$
g(u)=f(\mathrm{deg}(u))\prod_{v\in\mathrm{son}(u)}g(v),
$$

其中 $f(i)$ 表示 $i$ 条边两两匹配或者落单的方案数。

DP $f(i)$ 考虑最后一条的情况，

$$
f(i)=f(i-1)+(i-1)f(i-2).
$$

复杂度 $\mathcal O(n)$。

[submission(0)](https://uoj.ac/submission/520877)

## UOJ#196. 【ZJOI2016】线段树

[link](https://uoj.ac/problem/196)

拆贡献，$\mathrm{ans}_i=\mathrm{maxv}-\sum_v g_i(v)$，其中 $g_i(v)$ 为 $i$ 位置 $\le v$ 的方案数。

对于一个数 $i$，考虑它左边第一个比 $a_i$ 大的数的位置 $L$ 和右边第一个比 $a_i$ 大的数的位置 $R$，在操作过程中，这两个位置都会逐渐向 $i$ 紧缩。

记 $f(v,i,l,r)$ 表示前 $i$ 次操作后 $\max_{l\le i\le r}\{a_i\}\le v<\min\{a_{l-1},a_{r+1}\}$ 的方案数。转移就是讨论一次操作的区间和 $[l,r]$ 的相交情况，前后缀和优化，可以做到 $n^3q$。

数据随机的话，剪枝无用状态据说可以过？

每个 $v$ 的转移是一样的，考虑合在一起做，把方案数改为权值的贡献和，转移不变，复杂度 $\mathcal O(n^2q)$。

[submission(1)](https://uoj.ac/submission/520898)

## UOJ#140. 【UER #4】被粉碎的数字

[link](https://uoj.ac/problem/140)

乘法结果要记进状态里，考虑从低位向高位 DP。设 $f(i,d,\mathrm{more},\mathrm{diff})$ 表示前 $i$ 位，和 $R$ 大小关系为 $c$，乘法进位为 $\mathrm{more}$，$f(kx)-f(x)$ 为 $\mathrm{diff}$。

状态量 $20\times 2\times 1000\times 360$。

[submission(1)](https://uoj.ac/submission/520930)

## BZOJ#4230. 倒计时

[link](https://hydro.ac/d/bzoj/p/4230)

最优策略是每次减去当前最大的数字。

对于 $n=\overline{n_1n_2n_3\dots}$，和 $n$ 之前的最大值 $m$，让 $\overline{n_2n_3\dots}$ 减少至 $\le 0$，让 $n_1$ 退位，就是一个关于 $n'=\overline{n_2n_3\dots},m'=\max(m,n_1)$ 的子问题。

做记忆化搜索，状态量大约是 $\sigma^3$，$\sigma$ 是进制数。

[code(0)](https://gitee.com/renamoe/pastebin/blob/master/BZOJ4230.cpp)

## LOJ#6302. 「CodePlus 2018 3 月赛」寻找车位

[link](https://loj.ac/p/6302)

对行建线段树，每个节点代表区间内若干行形成的矩形。合并的时候计算跨过分界线的矩形的贡献，需要维护矩形两侧向内延伸的深度，然后单调栈计算。$\mathcal O(qm\log n)$。

[submission(1)](https://loj.ac/s/1325757)

## S2OJ#1188. 基因改造计划

[link](https://sjzezoj.com/problem/1188)

类似 [THUSC2016]成绩单 的挖串 DP。

先把所有模式串插入 trie 树。

区间 DP 内套子序列 DP，设 $g(l,r)$ 为区间 $[l,r]$ 挖下来的最大价值；$f(l,r,p)$ 表示区间 $[l,r]$ 最后一个字符所在子序列在 trie 树节点编号为 $p$，的最大价值。

$f$ 枚举子序列上一个位置进行转移，代价为 $g$。

最后再 DP 哪些段是会被挖的，就是最终答案。

复杂度 $\mathcal O(n^3m)$，但是有 $\frac 18$ 的常数，可以 AC。

[code(0)](https://gitee.com/renamoe/pastebin/blob/master/S2OJ1188.cpp)

## S2OJ#1182. 后宫

把 $s_1\to s_2$ 的链拎出来，每棵子树树形 DP，链上区间 DP。转移就是分配标号的多重集排列。

## S2OJ#1186. 庆典

考虑按小组大小排序，只用关心相邻小组不能相等，最后乘 $n!$。

每次令所有小组减去 $1$ 号小组的大小，转移为 $f(m,n)\gets\sum_{i\ge 1}f(m-1,n-i\times m)$。

只有 $n\le \frac{m(m+1)}{2}$ 时答案不为 $0$，加上前缀和优化，即可 $\mathcal O(n\sqrt n)$。

## S2OJ#1189. 求余数

观察性质，$<100$ 的质数有 $25$ 个，但是 $>50$ 的质数只能单独出现，只用考虑前 $15$ 个。

状压 DP，记 $g(i,S)$ 表示 $i$ 个数，质因子集合的并为 $S$，方案数。每次枚举一个 $1\dots m$ 的数做背包。注意到第一维的大小是不会超过 $|S|$。

对于多组询问，考虑把 $m=1\dots 100$ 的 $g(i,\cdot)$ 都处理出来，记为 $f(m,i)$。每次询问排列一下这些数就好了。

## S2OJ#1181. 创造题目

然后 $j$ 转移到 $i$ 的条件为

$$
\max_{j< k\le i}d_k\le i-j\le \min_{j< k\le i}u_k
$$

考虑 CDQ 分治，设 $\mathrm{su}_i$ 为 $i$ 到 $\mathrm{mid}$ 的前/后缀 $\min$，$\mathrm{sd}_i$ 为 $i$ 到 $\mathrm{mid}$ 的前/后缀 $\max$，可以得到

$$
\begin{cases}
j+\mathrm{sd}_j\le i\le j+\mathrm{su}_j\\
i-\mathrm{su}_i\le j\le i-\mathrm{sd}_i
\end{cases}
$$

二维偏序解决，总复杂度 $\mathcal O(n\log^2n)$。

[code(0)](https://gitee.com/renamoe/pastebin/blob/master/S2OJ1181.cpp)


## UOj#22. 【UR #1】外星人

[link](https://uoj.ac/problem/22)

操作序列存在 $a_i<a_j$，则 $a_j$ 无用。将 $a_i$ 从大到小排序，设 $f(i,j)$ 表示最小有用点为 $i$，$x=j$ 时的方案数，枚举下一个有用点 $k$ 转移，同时将中间的无用点排列在 $k$ 后面。复杂度 $\mathcal O(n^2x)$。

根据取模的性质，当 $x\to x'$ 时，$(x',x]$ 里的点都会变成无用点，$[1,x']$ 的点可能成为下一个有用点。意味着只需要记录 $j$ 即可，转移时将 $(j,j']$ 的无用点排列。复杂度 $\mathcal O(nx)$。

[submission(1)](https://uoj.ac/submission/522451)

## S2OJ#1178. 星际旅行

考虑计算每一段 $[i,i+1)$ 的答案，此时所有物品的概率可以写成关于纵坐标 $y$ 的多项式。做背包得到取 $0\dots n$ 个物品的概率的多项式，然后积分即可。

出于精度需求，要开 `long double`。

[code(1)](https://gitee.com/renamoe/pastebin/blob/master/S2OJ1178.cpp)

## S2OJ#1183. 分组

设两组集合为 $S,T$，$U=S\cup T$。

$$
\sum_{i\in S}r_i-\sum_{i\in T}l_i=\left(\sum_{i\in S}(l_i+r_i)\right)-\sum_{i\in U}l_i
$$

那么做背包即可得到所有可能的分组情况。需要 $\texttt{std::bitset<>}$ 优化。

注意是最差情况，更新答案时 $\sum_{i\in S}r_i-\sum_{i\in T}l_i$ 和 $\sum_{i\in T}r_i-\sum_{i\in S}l_i$ 要取 $\max$。

## S2OJ#1185. 基因改造问题

一个答案串可能对应多个划分方案，考虑在从前往后尽量让每段的右端点靠后的方案处统计。

子串匹配可以用 SAM 的自动机结构，SAM 上每个节点 $u$ 若 $\mathrm{trans}(u,c)=\mathrm{NULL}$，那么令其指向下一个串的 $\mathrm{trans}(\mathrm{root},c)$。然后在新的自动机上 DP 即可。

## S2OJ#1184. 攻城机变

~~题面不知道被谁改的没法看了。~~ 应该是攻者为 Z，御者为 W。 

首先得到的性质是：

- W 不会是预先设阵，应当是 W 和 Z 交替操作，因为这样 W 可以让 Z 多次折返；
- 每一行，W 设墙的位置一定是一个区间，比较显然。

区间 DP 记 $f_i(l,r,0/1)$ 表示到第 $i$ 行，Z 已经走过的位置为区间 $[l,r]$，位置在 $l$ 或者 $r$ 的答案。

每次 W 会考虑 Z 所在位置上方是否设墙，取 $\max$；对于每一种情况，Z 会考虑向左、右、上走，取 $\min$。

记忆化搜索实现比较方便，复杂度 $\mathcal O(nm^2)$。

## S2OJ#1190. 爱如摩天大楼

从后往前（从大到小）放会更好计算，每次只会影响第一段。

DP 设 $f(i,j,k)$ 表示从后往前放到第 $i$ 个数，第一段颜色为 $j$，已经产生了 $k$ 段的方案数。转移就是考虑第 $i$ 个数是否放在最前面，

$$
f(i,j,k)\gets \begin{cases}
(n-i)\cdot f(i+1,j,k) & j\neq c_i\\
(n-i+1)\cdot f(i+1,j,k)+\sum_{j'\neq c_i}f(i+1,j',k-1) & j=c_i
\end{cases}
$$

转移大部分地方是没有什么特殊变化的，设 $F(i,j,k)=\dfrac{f(i,j,k)}{(n-i)!}$，改写转移方程，

$$
F(i,j,k)\gets F(i+1,j,k)+[j=c_i]\left(F(i+1,j,k)+\sum_{j'\neq c_i}F(i+1,j',k-1)\right)
$$

另外维护一下 $\sum_j F(i,j,k)$ 那么每次从 $i+1$ 转移到 $i$ 只需要修改 $\mathcal O(k)$ 个位置。复杂度 $\mathcal O(nk)$。

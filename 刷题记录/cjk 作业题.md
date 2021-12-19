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

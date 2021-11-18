
## P4801 [CCO 2015]饥饿的狐狸

[link](https://www.luogu.com.cn/problem/P4801)

贪心。

最小值一定是大于 $W$ 和小于 $W$ 的分开处理，逐渐递增/递减最优。

最大值一定是从当前最大的和最小的之间反复横跳，左右分别用双指针扫，注意检查某一位之前加入喝水是否更优。

[code(0)](https://gitee.com/renamoe/pastebin/blob/master/LuoguP4801.cpp)

## Luogu P7677 \[COCI2013-2014#5\] LADICE

[link](https://www.luogu.com.cn/problem/P7677)

此类只有两条出边的二分图可以转化为只有右部点的图上连边。

若一个联通块为一棵树，一定存在一个空点，并且空点可以调整到任意位置。

如果联通块中产生环，所有点都被占有，后续在加入边一定失败。

并查集上打 tag 即可。

## Luogu P4443 \[COCI2017-2018#3\] Dojave

[link](https://www.luogu.com.cn/problem/P4443)

一个区间合法的条件是，设区间异或和为 $S$，存在 $S\operatorname{xor} x\operatorname{xor} y=U$ 并且 $x,y$ 一个在区间内、一个在区间外。

对于一个确定的区间，$S$ 确实，$x\operatorname{xor} y=S\operatorname{xor} U$ 也就确定。由于给出的是排列，每个数有唯一配对的另一个数。

如果区间长度为奇数，那么区间内至少一个点失配，一定存在一对合法的 $x,y$。

如果区间长度为偶数，假设区间内所有点都两两配对，那么 

$$
\begin{aligned}
S&=(x_1\operatorname{xor} y_1)\operatorname{xor} (x_2\operatorname{xor} x_2)\dots (x_k\operatorname{xor} y_k)\\
&=[2\nmid k](S\operatorname{xor} U)
\end{aligned}
$$

区间长度为某奇数的两倍也是一定合法的，那么只有长度为 $4$ 的倍数才无解，算一下这部分即可。

现在要求区间长度为 $4$ 的倍数并且区间内两两配对的数量。由于 $S$ 一定是 $0$，$x\operatorname{xor} y=U$，可以预先找到所有配对。考虑给每个配对的两个数赋相同的随机权值，下标按 $\bmod 4$ 分类进行统计。

[code](https://gitee.com/renamoe/pastebin/blob/master/LuoguP4443.cpp)

## LOJ#2753. 「CCO 2017」接雨滴

[link](https://loj.ac/p/2753)

入手点为最大值，最大值两边的水位只用考虑一个柱子的限制。不如将最大值放在第一位，因为任何一个方案都可以等价地调整到此。

然后对于所有方案，要计算的都是 $\sum_i \mathrm{sufmax}_i-h_i$，只需要关注 $\sum_i \mathrm{sufmax}_i$，只有单调栈上的点是有用的。

考虑单调栈上每个点的贡献。DP 记 $f(i,j)$ 表示前 $i$ 个柱子权值和为 $j$ 的可行性，从大到小每次尝试插入一个柱子 $h_k$，转移为

$$
f'(i,j)\gets f(i-t,j-t\times h_k)
$$

可以发现是完全背包的形式。同时使用 $\texttt{std::bitset<>}$ 优化可以做到 $\mathcal O(\frac{n^2h^2}{\omega})$。

[submission](https://loj.ac/s/1285084)

## Luogu P4657 \[CEOI2017\]Chase

[link](https://www.luogu.com.cn/problem/P4657)

同一路径两个方向的价值不一样，树形 DP $f,g$ 分别表示向上走和向下走的答案，然后拼接。

[code(2)](https://gitee.com/renamoe/pastebin/blob/master/LuoguP4657.cpp)

## Luogu P4786 \[BalkanOI2018\]Election

[link](https://www.luogu.com.cn/problem/P4786)

最优的方案是，从左到右扫，如果前缀和 $< 0$ 就删去当前点；从右往左再做一遍。

那么从左往右删去的点数也就是 $\min \mathrm{pre}_p$，从右往左删去的点数也就是 $\min \mathrm{suf}_q'=\min\{\mathrm{suf}_q-\min \mathrm{pre}_p+\min \mathrm{pre}_{p'< q}\}$。

答案即为

$$
\begin{aligned}
&\quad\min \mathrm{pre}_p+\min\{\mathrm{suf}_q-\min \mathrm{pre}_p+\min \mathrm{pre}_{p'< q}\}\\
&=\min \mathrm{pre}_p+\min\mathrm{suf}_q\quad(p<q)
\end{aligned}
$$

求最大子段和即可。

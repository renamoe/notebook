
咕的 F 题有点多怎么办啊。

## EDU69

[link](https://codeforces.com/contest/1197)

### C. Array Splitting 

相邻数连带权边，转化为去掉权值和最大的 $k-1$ 条边。

### D. Yet Another Subarray Problem

类似 $m=1$　的情况，代价 $- k \lceil \frac{r - l + 1}{m} \rceil$ 可以均摊到每 $m$ 个元素上。

对于确定的起点 $i$，令后面每个 $j\bmod m=i\bmod m$ 的点 $j$ 的权值减去 $k$ 即可。

那么做 $m$ 次。

### E. Culture Code

用 BIT 做一遍求出最小答案是容易的。然后在转移的时候同时记录方案数就好了。

就因为和最短路计数类似就打上 shortest paths 的标签？

### \*F. Coloring Game

每一列是独立游戏，考虑 DP 出来每一列每种 SG 函数值的方案数然后异或组合起来。

转移只影响三个格子，那么 SG 函数值值域 $[0,3]$，我们用 $4^3\times 4^3$ 的矩阵转移。预处理矩阵很容易。

每列遇到一段空白那么做矩阵快速幂，遇到有颜色的乘上对应矩阵，复杂度 $\mathcal O(64^3n\log a_i)$，过不去。

对于多次的矩阵快速幂，利用向量乘矩阵是 $\mathcal O(n^2)$ 的，预处理转移矩阵的 $2$ 的次幂，每次用向量直接去乘，复杂度降到 $\mathcal O(64^2n\log a+64^3n)$。

## EDU70

[link](https://codeforces.com/contest/1202)

### A. You Are Given Two Binary Strings...

尽量消去高位更优。

### B. You Are Given a Decimal String...

对应任意相邻两位 $a,b$ 以及任意自动机 $x,y$，处理出 $a$ 变成 $b$ 的最小步数。bfs 做同余最短路。

### C. You Are Given a WASD-string...

处理前后缀答案，枚举插入的东西然后拼接。

### \*D. Print a 1337-string...

用约数来拼不一定有解。

中间的 $3$ 能产生 ${x\choose 2}$ 的贡献，考虑将 $n$ 用 ${x\choose 2}$ 的变进制数表示。

### \*E. You Are Given Some Strings...

考虑每个位置作为 $s_i+s_j$ 中间分界点的贡献，那么只要求这个位置前面和后面匹配上的串数。

正着和倒着分别建 AC 自动机进行统计。

### \*F. You Are Given Some Letters...

设周期长度为 $k$，$\texttt a$, $\texttt b$ 分别出现 $a+b=k$ 次，假设 $\texttt a$, $\texttt b$ 个数量足够，一定可以构造出周期不为 $k$ 的约数的方案。

设周期循环 $\lfloor\frac{A+B}{k}\rfloor=p$ 次，$a,b$ 合法的条件为

$$
\begin{aligned}
p\times a\le A\le (p+1)\times a\\
p\times b\le B\le (p+1)\times b\\
\end{aligned}
$$

注意是 $\le$，暂时只关心 $a,b$ 以及 $k$ 的合法性，不考虑是否算重。

化简为限制 $a,b$ 的式子，

$$
\begin{aligned}
\left\lceil\frac{A}{p+1}\right\rceil\le a\le \left\lfloor\frac{A}{p}\right\rfloor\\
\left\lceil\frac{B}{p+1}\right\rceil\le b\le \left\lfloor\frac{B}{p}\right\rfloor\\
\end{aligned}
$$

那么枚举 $p$，可以得到 $a,b$ 的合法范围。

对于每个 $p$，$k$ 的限制也是一个区间，可以整除分块，复杂度 $\mathcal O(\sqrt{A+B})$。


## CF749

[link](https://codeforces.com/contest/1586)

### A. Windblume Ode

如果是质数（奇数），说明 $a$ 序列中至少存在一个奇数，减去它变成偶数就好了。

### B. Omkar and Heavenly Tree 

最好是让 $a,c$ 尽量接近，可以想到建一个虚点为根，造一个菊花图。

重要性质是 $m < n$，那么存在至少一个点不受任何“不能在两点路径上的限制”，令其为根。

### C. Omkar and Determination 

如果一个格子上方和左方存在可退出的格子，该格子能否可退出和格子是否为填充，可以唯一对应。

如果上方和左方都不可退出，该格子无论是否填充都会呈现为不可退出。

那么只要寻找子矩阵中是否存在一个格子左方和上方都为 $\texttt X$。

### D. Omkar and the Meaning of Life 

一个容易想到的构造是让所有数增加 $k$，然后让 $p_i$ 增加 $k-1$，那么如果 $p_i-1$ 在 $p_i$ 前面，可以找到 $p_i-1$ 的位置。

由于 smallest 的限制，我们只操作最后一个元素。让所有数都增加 $n$，$p_n$ 增加 $n-k$，那么可以找到 $p_n-k$ 在哪里，直到找不到便确定了 $p_n$ 是多少。往上也是类似。

### E. Moment of Bloom 

放到树上是非常好做的，那么考虑转化到树上。

把边的权值放到相邻的两个点上，每次操作一定只会改变 $x,y$ 两个点的奇偶性。如果最后所有点都为偶数，那么一定有解。只要让任意两点的路径唯一就能满足，那么从图上随便拎出一个生成树。

如果最后不满足，那么为奇数的点一定有偶数个，两两配对即可。我当时想的麻烦，在树上做了遍 DP，也是可以的。

### \*F. Defender of Childhood Dreams 

$k$ 个点，任意一条路径长度不超过 $k-1$，那么可以都染成一种颜色。

扩展到 $n$ 个点，每 $k$ 个点分为一段，那么跨过段与段之间的路径会超过 $k$ 条边，那么段与段之间的边染成另一种颜色。于是转化为 $\left\lceil\frac{n}{k}\right\rceil$ 个点的子问题。

颜色相同的路径一定在同一层的同一段，长度至多为 $k-1$，同时是最优。

答案也就是 $\lceil\log_kn\rceil$，按上述方法构造即可。

G,H,I 题随缘补题。

## EDU71

[link](https://codeforces.com/contest/1207)

### D. Number Of Permutations

直接求不好求，容斥一下，求一下两维分别有序的方案数，**如果有交的话**再算一下两维同时有序的部分。

### E. XOR Guessing

如果全是 $0$ 就好了，但是不让相同的话这怎么猜啊？

高 $7$ 位和低 $7$ 位分别做就好了。

### F. Remainder Problem

根号分治典中典。

### \*G. Indie Album

对 $t$ 串集合建立 AC 自动机，询问离线，在 $s$ 串的 trie 树上 dfs 维护 trie 树上一条路径代表的一个串的答案。

dfs 时当前在 AC 自动机上的节点会对 fail 树上它的所有祖先产生一次贡献，转化为树链加单点查问题。

## EDU72

[link](https://codeforces.com/contest/1217)

### C. The Number Of Good Substrings

只有 $\log n$ 位是有用的，另外处理每个位置前面 $0$ 的个数即可找到某个值对应的范围。

### \*D. Coloring Edges

如果给出的图没有环，答案为 $1$；否则每个环一定存在至少一个从编号大的点到编号小的点的边、一个从编号小的点到编号大的点的边，给两类边分别染一个颜色。

或者可以在 DFS 树上考虑，一个环要经过至少一条树边和恰好一条反祖边，给所有返祖边染第二种颜色。

### \*E. Sum Queries?

一个集合不合法的充要条件是存在某两个数某一位同时不为 $0$，即使进位也会影响更高位。

只需要考虑两个数的集合，那么可以线段树，每个区间对十进制每一位记录包含该位最小的数，即可合并两个区间的答案。

### \*F. Forced Online Queries Problem

动态图连通性经典题，但我们不用大数据结构。可以发现是伪强制在线，每次给出的边有两种可能。

- 做法 1

考虑分块，将询问在一个块内的一起处理。那么将这个块中可能影响的边拎出来，块之前的边就可以直接加入并查集，每次修改或询问，只用遍历 $\mathcal O(B)$ 条边，用可撤销并查集维护。

复杂度 $\mathcal O(\frac{m^2}{B}\log n+mB\log n)$。

- 做法 2

还是线段树分治，把所有可能的边都考虑进来，时间维上形成线段。在线段树上边遍历边加边，每一次询问可以确定该点开头的线段是否加入。复杂度 $\mathcal O(m(\log n+\log m))$。

## CF751

[link](https://codeforces.com/contest/1601)

### A. Array Elimination

每一位的答案取交集。

### B. Frog Traveler

线段树优化建图，然后 01-BFS。

### C. Optimal Insertion

- 做法 1

首先把 $b$ 序列排序，可以发现最优决策点 $p_i$ 单调不降。

证明考虑一对点 $b_i < b_j$，若 $p_i > p_j$，交换会使答案更优。

那么分治解决。计算某个 $b_x$ 在分治区间内每个点的逆序对个数：区间以外的部分用主席树，区间内扫一遍。复杂度 $\mathcal O(n\log n)$。

- 做法 2

对于一个数 $b_i$，将 $<b_i$ 的所有 $a_j$ 标为 $0$，$>b_i$ 的标为 $1$，那么统计答案只要维护每个位置前后 $0/1$ 的个数。

那可以放到线段树上，两个序列都排序，从小到大增量修改。

## EDU73

[link](https://codeforces.com/contest/1221)

没什么精神，要反思一下。

### C. Perfect Team

对于只有 $c,m$ 非零的情况，二分可以找到最值。

发现犯傻了，$c,m$ 不相等时，多出来的部分可以看作第三类人；$c=m$ 时最大的答案就是 $\lfloor\frac{c+m}{3}\rfloor$。

### D. Make The Fence Great Again

结论是每个点增加的高度不超过 $2$，因为 $+3$ 及以上可以被 $+0,+1,+2$ 代替。

那么可以直接 DP。

### \*E. Game With String

给线段按长度分类：

- $x < b$，两人都不能操作；
- $b\le x < a$，只有 Bob 能操作一次；
- $a\le x < 2b$，Alice 和 Bob 都能操作一次；
- $2b\le x$，其他情况。

第一类是可以无视的。

如果出现第二类线段，那么一定后手必胜，因为 Alice 能操作的线段 Bob 都能，最后一定会达到只剩下第二类线段的情况，只有 Bob 能操作。

由上面可以推得，如果 Alice 操作之后还存在第四类线段，那么 Bob 可以通过这个线段创造一个第二类的。所以存在两个及以上第四类也是后手必胜。

剩下的情况中，如果没有第四类，那么也就只剩下第三类，答案取决于第三类线段数量的奇偶性。

如果有一个第四类，Alice 可以将其分割成两个线段，$\mathcal O(n)$ 枚举一下所有分割的情况，看是否存在 Alice 必胜的情况。

### \*F. Choose a Square

一个点 $(x,y)$ 被算入 $[l,r]$ 贡献的条件为 $l\le \min(x,y)\le\max(x,y)\le r$。

枚举右端点 $r$，我们要算 $\sum_i c_i+l-r$ 最小值。按 $\max(x,y)$ 不断加入点到 $\min(x,y)$ 上，用线段树维护区间加减和查询 $\sum_i c_i+l$ 的最小值和位置即可。

需要离散化。

### \*G. Graph And Numbers

先容斥放宽限制，设 $f(S)$ 表示边权均属于集合 $S$ 的方案数，那么答案为 $f(\{0,1,2\})-f(\{0,1\})-f(\{1,2\})-f(\{0,2\})+f(\{0\})+f(\{1\})+f(\{2\})-f(\{\})$。

- $f(\{0,1,2\})$：$2^n$；
- $f(\{0,1\}),f(\{1,2\})$：两者本质相同，不太好直接求；
- $f(\{0,2\})$：即不存在 $0-1$ 边，每个联通块染一个颜色，$2^{\mathrm{cnt}}$；
- $f(\{0\}),f(\{2\})$：全部染成一个颜色，但是孤立点随意，$2^{\mathrm{ind}}$；
- $f(\{1\})$：如果是二分图，则为 $2^{\mathrm{cnt}}$，否则 $0$；
- $f(\{\})$：图中存在边为 $0$，否则 $2^n$；

那么考虑求 $f(\{0,1\})$：

要求染为颜色 $1$ 的点两两之间无边，我们有 $\mathcal O(2^n)$ 处理所有合法点集的做法。

$n=40$ 考虑折半，分成两个点集分别处理合法点集，对于点集 $1$ 的每个合法子集，通过遍历其所有点的边，可以找到点集 $2$ 中不能共存的子集。然后只要对点集 $2$ 做子集和，高维前缀和或者 FWT 即可。

复杂度 $\mathcal O(n2^{n/2})$。



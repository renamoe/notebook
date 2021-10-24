
咕的 F 题有点多怎么办啊。

## EDU69

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



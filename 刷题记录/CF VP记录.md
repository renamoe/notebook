
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

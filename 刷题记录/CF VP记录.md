
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



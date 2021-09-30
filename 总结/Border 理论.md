## 相关

约定，$n=|S|$，字符串 $S$ 下标范围 $0\dots n-1$，用 $S[i,j)$ 表示区间 $[i,j)$ 形成的子串。

Border：前缀 $S[0,m)$ 满足 $S[0,m)=S[n-m,n)$ ；

周期：$p$ 满足 $\forall i\ge p$, $S[i]=S[i-p]$；

整周期：周期 $p$ 满足 $p|n$；

---

## Border 的性质

### 定理 1

若 $Border(S)$ 表示 $S$ 所有 Border 的集合，$Border(S)_{\max}$ 表示其最长 Border，那么
$$
Border(S)=\{Border(S)_\max\}\cup Border(Border(S)_\max)
$$

---

### 定理 2

WPL 定理：

对于 $S$ 的周期 $p,q$，若 $p+q\le n$，那么 $\gcd(p,q)$ 也是 $S$ 的周期。

---

### 定理 3

若 $S$ 为 $T$ 的前缀，$S$ 有整周期 $p$，$T$ 有周期 $q$（$q\le |S|$），且 $p|q$，那么 $T$ 有周期 $p$。

---

### 定理 4

若 $S$ 为 $T$ 的 Border，且 $|S|\ge \frac 12 |T|$，那么 $T$ 有周期 $|T|-|S|$。

---

### 定理 5

若 $|S|\ge \frac 12 |T|$，那么 $S$ 在 $T$ 中的匹配位置为等差数列。

---

### 定理 6

若 $S$ 最长 Border 的长度 $L\ge \frac 12 n$，那么所有长度 $\ge \frac 12n$ 的 Border 按长度排序，构成等差数列，公差为 $n-L$。

---

### 定理 7

串 $S$ 的所有 Border 按长度排序，构成 $\mathcal O(\log n)$ 段等差数列。

---

## 回文 Border

### 定理 1

回文串的回文后缀与 Border 对应。

同时回文串的回文后缀也就有了 Border 的所有性质。

---

### 定理 2

若串 $S$ 有周期 $p$，那么 $S$ 的一个循环节一定可以被拆成两个回文串，长度为 $|S|\bmod p$ 和 $p-(|S|\bmod p)$。

---

### 定理 3

若串 $S$ 的最长回文后缀为 $T$，且 $|T|\ge \frac 1 2|S|$，那么 $T$ 在 $S$ 只会匹配两次，分别为前缀和后缀。

---

## 参考

- [Border理论小记 - command_block](https://www.luogu.com.cn/blog/command-block/border-li-lun-xiao-ji)
- [回文自动机小记 - command_block](https://www.luogu.com.cn/blog/command-block/hui-wen-zi-dong-ji-xiao-ji)


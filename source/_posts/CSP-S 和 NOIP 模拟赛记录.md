---
title: CSP-S 和 NOIP 模拟赛记录

mathjax: true

tags: 比赛记录

categories: 比赛记录

excerpt: 记录 CSP-S2024 和 NOIP2024 前的模拟赛训练。
---

## 9.18（by lanos212）

T1 签到，10 mins 内过了。

T2 乍一看有点困难，题目太形式化，不太直观，先跳过去思考 T3 了，T3 没有什么 DP 的思路，但是这种题显然需要 DP。

看了一眼 T4，被一堆式子糊脸恶心了，没有怎么思考。

接下来一个小时在思考 T2 和 T3，突然发现 T2 只需要每次求最短路就可以了，那么就是简单的，但是乍一看自己写的好像是 $O(n^4)$  的，但是每个点只会被更新 $O(n)$ 次，那么均摊就是 $O(n^3)$ 的了，感觉这个题浪费这么多时间真的不太应该。

然后冷静下来看 T4，发现需要 DP，看到区间最小值考虑按照笛卡尔树来 DP，想了一下会了 $O(n^2)$ ，直接写就过了，最后还剩下一个小时左右去攻克 T3。

但是自己根本没有往**组合意义**那方面想，也就是把所有方案的权值和双射到计算另一种方案上。

题目中的 $\prod c_i$ 可以看作每个小狗选一个最喜欢的，那么就可以设出一个 DP，$f_{i,j}$ 表示前 $i$ 天，已经有 $j$ 只狗得到了喜欢的香肠的方案。
$$
f_{i,j} \to f_{i+1,j+k}\binom{n - j}{k}\binom{n - j - k}{a_{i+1} - k}
$$
最终得分：$100+100+44+100=344$，rank 8。

## 9.25（by Mine_King）

T1 签到，但是磨蹭了一下，到 20 分钟才确定过了。

T2 读题花了很久，先会了一个暴力 DP，**发现在根大于儿子的时候下面都是确定的**，于是可以建立重构树，据 @喵仔牛奶 说这种东西叫“树上笛卡尔树”，反正改完之后直接 DP 就可以了，这个题做了 2h，问题可能在于没有快速发现上面那个加粗的性质吧。

T3 没有任何的观察，不会任何多项式做法，实际上后两题都是我薄弱的字符串 Border 理论相关。

T3 给出的这个每个字符出现至多 $2$ 次，可以得到这个串**只有一个长度小于等于一半的 Border**，证明直接反证。

对于 Border 相同的字符串 $P = ABA$，计算 $f(S,P)$ 的时候只考虑 $S$ 中若干个 $ABABA...ABA$ 的极长子串，设有 $x$ 个 $A$，那么答案是 $\left \lfloor \dfrac{x}{2} \right \rfloor$，感受到计算这个只和 border 长度有关，不关心填了什么，那么直接枚举这个长度，然后问题变成计算 $f(S,P)$ 和计算 border 为 $len$ 的 $P$ 的个数。

#### 计算 $f(S,P)$

在 $len = 0$ 的时候答案就是 $(n-m+1)V^{n-m}$。

那么直接容斥，计算 $\sum \limits_{i=1} (-1)^{i-1} S(A(BA)^i)$，$S()$ 表示直接计算的答案。

#### 计算 border 为 $len$ 的 $P$

直接枚举中间部分出现两次的字符个数。

因为 $V \le 10^9$，所以需要化一下式子，变成只和 $V$ 的不超过 $m$ 次下降幂有关。

T4 其实关键在于 Significant Suffixs 只有 $\mathcal{O}(\log n)$ 个，然后是好做的，只需要一个 $\mathcal{O}(\sqrt n) - \mathcal{O}(1)$ 的分块即可。

最终得分：$100+100+5+10=215$，rank 9。

## 9.28（by cyfff）

T1 直接过了。

T3 想了一下发现可以区间 DP，那么也过了，这个时候 9：00，还有两个多小时。

T2 先做了一些错误的尝试，然后发现只能记录留下来的两张牌，写了一个暴力 DP，发现只转移存在值的点似乎很快？但是实际上复杂度是错误的，在这里花费了一点时间做无意义的尝试。

冷静下来发现 DP 的转移量远小于状态量，想到之前做过的类似题，那么直接转移可能的转移就是对的？

写了一下发现过了大样例，但是已经快 11 点了，T4 看了一下发现是个容斥状物，但是先打算写 T2 拍子，写完发现没过拍！

冷静，发现是全局加 $1$ 的时候标记打错了，调了 30mins。

最后 20 mins 极限冲了一下 T4 的两个暴力分。

**但是，T3 fst 了！！！1**

原因是常数太大，小机房机子太慢，导致的 TLE，虽然做法是常数非常小的，但是因为寻址的不连续，导致很慢。

最终得分：$100+100+54+34=288$，rank 9。

不 fst 就是 $334$ + rank 4 了/kk。

感觉目标是省选的话这个分和排名还是不够啊，需要加训点比赛了。

## 9.30（by cqbz)

T1 签到，但是对于这个结论还是稍微犹豫了一下。

T2 构造，但是发现并不难，先会了 $3n+4$ 的做法，然后发现 $n=300$ 可以直接构造，这时候 9 点。

然后花了 2h 在 T3 和 T4 上来回游走，发现一个题都不会，T3 以为自己会了 $\mathcal{O}(n^2\log n)$ 的解法，但是调了很久才发现假了。

最后留给暴力的时间不多，只有比较基础的 $45+25$ 暴力，写着写着发现会 T4 了，但是是个码量比较大的题，导致完全写不完，最后遗憾离场。

最终得分：$100+100+45+25=270$，rank 4。

发现很多人被 T2 创飞了，但是自己明明没有被创到还是分数不高？关键在于没有快速认识到 T4 是简单题，属于是被 T3 创飞了，没想到 T3 大家都不会。

## 10.5 （by edge）

T1 简单题，10mins 过了。

T2 想到了二进制分组，但是没有想到按照最高位来区分，写了随机乱搞居然过了。

T3 这种题一看就是把括号序列转化成 $1$ 和 $-1$，但是没有去分析一个路径和括号序列的对应关系，而是直接去考虑直径了，实际上考虑范围可以不用一步到位。

T4 是经典的双射计数题，自己已经推出了双射的情况，但是没有简化，导致无从下手。

最终得分：$100+100+55+25=280$，rank 6，被开挂哥超了/lh。

## 10.6 （by grass8cow）

T1 是简单的。

T2，T3，T4 看过之后感到非常困难，T2 是结论题，但是没有什么想法，T3 是一个组合意义题，看来比较可做，T4 是一个 ds，感觉和之前做过的题有点像，但是也不好直接转化。

于是先冲了一下 T3，发现题目两个组合对象是无标号的，然后自己推成有标号的了，导致一直没有做出来，发现错误后考虑了 DP，但是没有得到什么和 $n$ 无关的 DP。

但是第一步的组合意义就转化的不够彻底，这种“分界”的形式可以引入一个新的组合对象来实现。

然后将所有的 DP 式子列出来就可以得到一个和 $n$ 无关的转移式子。

T2 的结论通过部分分可以得到和二分图有关，但是不清楚有什么关系，当时一直在硬推，但是没有去做第一步的转化，也就是将点权和颜色绑定，否则是很难同时处理两个对象的，但是我当时一直在想如何固定一个移动另一个，这实际上是后面的工作了，另外和二分图相关的结论可以去考虑如果存在奇环会怎么样。

T4 就是要不断找最优的情况。

这种多个线段问题，往往考虑区间没有包含的情况，也就是左右端点都递增，这个问题中显然包含别的线段的线段不优。

于是只需要前驱后继，使用 ``set`` 可以维护，还需要用拓扑排序处理包含的情况，代码比较难写。


最终得分：$100+0+30+40=170$，rank 8。

## 10.7 （by qdez）

T1 想了一下过了，花了 20mins，当时感觉这个题比较容易挂分，打算打个对拍，但是没打。

T2 不会一点，第一步转化成平面上的问题就没想到，可能想到了，但是以为要矩形加法导致不会了，感觉降智严重。

排列问题无非就是考虑二维平面和置换环。

T3 很快发现了答案是每个点两边取 $\min$ 加起来，但是不会维护了，自己以为是考虑增量，但是实际上就是把原来的减掉然后再加上新的，使用倍增即可。

T4 是一个有后效性的 DP，显然使用高斯消元法，但是如果对于所有东西消元的话只能过 $80$ 左右，实际上可以只对答案数组消元，因为其他的 DP 转移都没有后效性，提前预处理就可以了。

最终得分：$90+60+36+72=258$，rank 5，T1 因为输入了 $n \times n$ 的矩阵导致挂了 $10$ 分，T4 取模搞出负数又是 $8$ 分，但是一题不过能 rk5 有点吃惊。

## 10.12（by gdsy）

最傻逼的一集。

T1 主席树板子。

T2 不会。

T3 直接暴力的复杂度就是对的。

T4 直接网络流。

## 10.14（by wenmo）

我的模拟赛。

## 10.16（by wmic.）

T1 和 T2 是签到题，稍加推理后便通过了，此时 9:00 左右。

T3 直觉是一道欧拉路题，根据差最多为 $1$ 也可以发现，事实上也确实如此，但是自己并没有任何的方向，没有全力探究 $S = 2$ 的性质，导致无法进一步推算。

T4 是比较困难的题，直接暴力拿了 $56$ 分，实际上专注 $l + 1 = r$ 的性质也不难做出来。

最终得分：$100+100+15+56=271$，rank 4，T3 的发挥还是太差了。

## 10.17（by szzx）

$4$ 题超纲了 $3$ 个？？？

T1 和 T3 题目都表述不清，导致我浪费了很多时间没有通过。

T2 较板，但是学会了 Manacher 求解本质不同回文子串。

T4 是较为巧妙的 DP，但是思考时间不多，比较遗憾。

最终得分：$40+60+20+10=130$，rank 14。

## 10.18（by cqbz）

T1 是简单的，T2 很快发现了等价条件，然后直接计数是 $O(n^2)$ 的，需要 bitset 优化，但是并没有想到合适的方法，实际上应该去转换 DP 方式。

T3 std 23k。

T4 是较为简单的题，但是一开始忽略了 $h_{i, 1} = c_i$，导致比较难做，最后仅仅得到了 $15$ 分。

最终得分：$100+80+0+15=195$，rank 11，感觉失误较大。

## 10.21（by tyr）

T1 花了 $15$ 分钟。

T2 思考了很久，在 $1.5$ 小时后写出了一个能过全部大样例的做法。

T3 读完就秒了，写了一会但是卡常数了很久，最后用 fread 导致 MLE 了/ll。

T4 没来得及做什么思考。


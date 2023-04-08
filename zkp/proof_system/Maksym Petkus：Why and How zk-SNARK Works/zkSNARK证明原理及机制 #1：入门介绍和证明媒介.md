*原文：<Why and How zk-SNARK Works 1: Introduction & the Medium of a Proof>*

*翻译：Junwei*

> *这篇文章是**[PDF 版本](https://arxiv.org/abs/1906.07221)**的修订版。*

尽管已经有多个关于构建*zkSNARK的*重要资源，包括论文原文[ [Bit+11](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#d914) ; [Par+13](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#4d29) ] ，以及讲解版本[[Rei16](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#eabb); [But16](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#91fa); [But17](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#3df0); [Gab17](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#d309)]，由于零知识证明有大量的可拆解组件，其对许多人来说仍然是一个黑匣子。虽然他们给出了一些拼图，但如果没有缺失的部分，就无法看到完整的图片。

笔者第一次发现zkSNARK的各个组件是如何很好地组合在一起的，就被数学之美所震撼，看到的维度越多，就越好奇。因此，本文的重点是分享学习经验，用简单明了的方法，通过示例来阐明*zkSNARK，*并在此过程中回答许多问题，以便更多的人能够理解这项最先进的技术、其创新者以及最终的数学之美。

这项工作的贡献是一个具有足够复杂程度的简单说明，这是理解*zk-SNARK*所必需的，而无需任何主题、密码学或高等数学的先决知识。主要目标不仅是解释它是如何工作的，而且是解释它为什么工作以及它是如何变成这样的。

# 前言

虽然最初计划用较短的篇幅，但现在文章已经超过了几十页，不过它需要的前置知识很少，并且可以随意跳过熟悉的部分。

如果你不熟悉一些使用的数学符号，请不要担心，这里只会介绍一些，而且会逐步介绍，一次介绍一个。

# 介绍

*简洁非交互式零知识证明*（*zkSNARK*）巧妙的地方在于，可以在不透露任何其他信息的情况下证明某些事情是真的，但是为什么它首先有用呢？

*零知识证明*在无数应用中都有优势，包括：

1）证明隐私数据的声明：

- A*的*银行账户超过*X*
- 去年，一家银行没有与实体*Y进行过交易*
- 在不暴露完整 DNA 的情况下匹配 DNA
- 信用评分高于*Z*

2）匿名授权：

- 证明请求者*R*有权访问网站的受限部分而无需透露其身份（例如，登录名、密码）
- 证明个人来自允许的国家/州列表，但不透露具体来自哪个国家/州
- 证明个人拥有地铁/地铁的月票，而无需透露卡的 ID

3）匿名支付：

- 完全脱离任何身份信息的支付 [ [Ben+14](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#4c0c) ]
- 纳税而不透露自己的收入

4）外包计算：

- 外包昂贵的计算并验证结果是否正确而无需重新执行；它开辟了一种无需信任的计算
- 将区块链模型从每个节点计算相同的运算，变更为一方计算而其他人都验证

表面上听起来非常厉害，但底层方法是数学和密码学的“奇迹”，自1985年在主要著作“交互式证明系统的知识复杂性”[GMR85]引入以来，已经进行了四十年的研究。随后引入了非交互式证明[[BFM88](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#1bde) ]，这在区块链的背景中尤为重要。

在任何*零知识证明*系统中，都有一个*证明*者想要在不透露任何其他信息的情况下说服*验证者，*某些*声明是真的。例如，验证者只知道证明者*在他的银行账户中余额超过*X*但没有别的信息（即未披露实际金额）。一个零知识证明协议应该满足三个属性：

- 完整性 — 如果声明为真，那么*证明者*可以说服*验证者*
- 可靠性 — 作弊的*证明者*无法说服*验证者*相信虚假声明
- 零知识 — 交互仅透露声明是否为真，仅此而已

*zk-SNARK*术语本身是在[[Bit+11](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#d914)]中引入的，它建立在[[Gro10](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#e2e7) ]的基础上，随后的匹诺曹(Pinocchio)协议[[Gen+12](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#7f22); [Par+13](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#4d29)]使其适用于通用计算。

# 证明的媒介

让我们从简单形式开始，尝试证明一些东西，而不用担心零知识、非交互性、它的形式和适用性。

想象一下，我们有一个长度为10的位数组，我们想向验证者（例如程序）证明所有这些位都设置为了1。

![img](1-1.webp)

验证者一次只能检查（即读取）一个元素。为了验证该陈述，可以通过以任意顺序读取元素并检查它是否真的等于 1 来继续进行，如果等于1，则在第一次检查后该声明的可信度为⅒= 10%，验证者必须继续下一轮，直到他达到足够的置信度，如果一旦等于0则整体验证失败。在某些情况下，人们可能信任证明者并且只需要50%的可信度，这意味着必须执行 5 次检查，而在其他需要95%的可信度的情况下，必须检查所有单元格。很明显，这种证明协议的缺点是必须进行与元素数量成比例的检查，如果我们处理数百万个元素的数组，这是不切实际的。

让我们考虑多项式，它可以可视化为图形上的曲线，由数学方程式构建：

![img](1-2.webp)

上面的曲线对应于多项式：*f*(*x*) = *x*³ – 6*x*² + 11*x* – 6。多项式的次数由*x*的最大指数决定，在本例中为3。

*多项式有一个有用的性质，即，如果我们有两个次数为d*的不相等多项式，它们最多只能在*d个*点上相交。例如，让我们稍微修改原始多项式*x* ³ – 6*x* ² + **10***x* – **5**并将其可视化为绿色：

![img](1-3.webp)

如此微小的变化会产生截然不同的结果。事实上，不可能找到两个不相等的多项式，它们会共享曲线的连续部分（不包括交点）。

此属性源自查找交点的方法。如果我们想找到两个多项式的交集，我们需要使它们相等。例如，要找到多项式与*x*轴的交点（即*f*(*x*) = 0），我们将*x*³ – 6*x* ² + 11*x* – 6 = 0，这样一个方程的解将是那些交点：*x* = 1、*x* = 2 和*x* = 3，你也可以清楚地看到在上一张图中也是如此，其中蓝色曲线与*x*轴线相交。

同样，我们可以将多项式的原始版本和修改后的版本构建等式，以找到它们的交点。

$$
x^3-6x^2+11x-6=x^3-6x^2+10x-5
$$
所得多项式的次数为1，显而易见解*x*=1。因此只有一个交点：

![img](1-4.webp)

对于任意次数*d的多项式，任何此类方程的结果始终是次数最高为d*的另一个多项式，因为没有乘法会产生更高的次数。例如：5*x* ³ + 7*x* ² – *x* + 2 = 3*x*³ – *x*² + 2*x* – 5，可简化为 2 *x* ³ + 8 *x* ² – 3 *x* + 7 = 0。代数基本定理告诉我们一个*d*次多项式最多可以有*d*个解（在接下来的部分中会详细介绍），因此最多有*d*个交点。

因此我们可以得出结论，在在任意点对任何多项式的求值（更多关于多项式求值：[ [Pik13](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160#489a) ]）类似于其唯一身份的标识。让我们在*x*=10处计算示例中的多项式。

$$
x^3-6x^2+11x-6=504
x^3-6x^2+10x-5=495
$$
事实上，在要求值的*x*的所有选择中，最多只有3个选择在这些多项式中具有相同的求值，而所有其他选择的x上求值都会不同。

这就是为什么如果证明者声称知道验证者也知道的某个多项式（无论其次数有多大），他们可以遵循一个简单的协议：

- *验证者为x*选择一个随机值并在本地进行多项式求值
- 验证者将*x*提供给证明者并要求计算所讨论的多项式
- 证明者计算他在*x*处的多项式并将结果提供给验证者
- 验证着检查本地结果是否等于证明者的结果，如果是，则声明被证明具有高可信度

例如，如果我们考虑*x*从 1 到 10⁷⁷ 的整数范围，则多项式求值不同的点数为10⁷⁷ – *d*。因此*， x*意外“命中” *d*个交点中的任何一个的概率等于（被认为可以忽略不计）：

$$
\frac{d}{10^{77}}
$$

> *注意：与低效的位检查协议相比，新协议只需要一轮，并且可以给出极高的可信度（假设d充分小于x取值范围的上限 ，几乎是100% ）。*

这就是为什么多项式是*zk-SNARK*的核心，尽管其他证明媒介也可能存在。

# 参考资料

1. [Bit+11] — Nir Bitansky, Ran Canetti, Alessandro Chiesa, and Eran Tromer. *From Extractable* *Collision Resistance to Succinct Non-Interactive Arguments of* *Knowledge, and Back Again*. Cryptology ePrint Archive, Report 2011/443. https://eprint.iacr.org/2011/443. 2011
2. [Par+13] — Bryan Parno, Craig Gentry, Jon Howell, and Mariana Raykova. *Pinocchio: Nearly Practical Verifiable Computation*. Cryptology ePrint Archive, Report 2013/279. https://eprint.iacr.org/2013/279. 2013
3. [Rei16] — Christian Reitwiessner. *zkSNARKs in a Nutshell*. 2016. url: https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/ (visited on 2018–05–01)
4. [But16] — Vitalik Buterin. *Quadratic Arithmetic Programs: from Zero to* *Hero*. 2016. url: https://medium.com/@VitalikButerin/quadratic-arithmetic-programs-from-zero-to-hero-f6d558cea649 (visited on 2018–05–01)
5. [But17] — Vitalik Buterin. *zk-SNARKs: Under the Hood*. 2017. url: https://medium.com/@VitalikButerin/zk-snarks-under-the-hood-b33151a013f6 (visited on 2018–05–01)
6. [Gab17] — Ariel Gabizon. *Explaining SNARKs*. 2017. url: https://z.cash/blog/snark-explain/ (visited on 2018–05–01)
7. [Ben+14] — Eli Ben-Sasson, Alessandro Chiesa, Christina Garman, Matthew Green, Ian Miers, Eran Tromer, and Madars Virza. *Zerocash: Decentralized* *Anonymous Payments from Bitcoin*. Cryptology ePrint Archive, Report 2014/349. https://eprint.iacr.org/2014/349. 2014
8. [GMR85] — S Goldwasser, S Micali, and C Rackoff. “The Knowledge Complexity of Interactive Proof-systems”. In: *Proceedings of the Seventeenth Annual ACM* *Symposium on Theory of Computing*. STOC ’85. Providence, Rhode Island, USA: ACM, 1985, pp. 291–304. isbn: 0–89791–151–2. doi: [10.1145/22145.22178](https://doi.org/10.1145/22145.22178). url: http://doi.acm.org/10.1145/22145.22178
9. [BFM88] — Manuel Blum, Paul Feldman, and Silvio Micali. “Non-interactive Zero-knowledge and Its Applications”. In: *Proceedings of the Twentieth Annual ACM* *Symposium on Theory of Computing*. STOC ’88. Chicago, Illinois, USA: ACM, 1988, pp. 103–112. isbn: 0–89791–264–0. doi: [10.1145/62212.62222](https://doi.org/10.1145/62212.62222). url: http://doi.acm.org/10.1145/62212.62222
10. [Gro10] — Jens Groth. “Short pairing-based non-interactive zero-knowledge arguments”. In: *International Conference on the Theory and Application of Cryptology and* *Information Security*. Springer. 2010, pp. 321–340
11. [Gen+12] — Rosario Gennaro, Craig Gentry, Bryan Parno, and Mariana Raykova. *Quadratic* *Span Programs and Succinct NIZKs without PCPs*. Cryptology ePrint Archive, Report 2012/215. https://eprint.iacr.org/2012/215. 2012
12. [Pik13] — Scott Pike. *Evaluating Polynomial Functions*. 2013. url: http://www.mesacc.edu/~scotz47781/mat120/notes/polynomials/evaluating/evaluating.html (visited on 2018–05–01)
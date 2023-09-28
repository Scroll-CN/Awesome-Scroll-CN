*原文：<Why and How zk-SNARK Works 8: Zero-Knowledge Computation>*

*翻译：Junwei*

# 零知识计算证明

自从引入通用计算协议（[运算证明部分](https://medium.com/@imolfar/why-and-how-zk-snark-works-4-general-purpose-computation-dcdc8081ee42#7196)）以来，我们不得不先舍弃*零知识*属性，以使转换过程更简单。到目前为止，我们已经构建了一个可验证的计算协议。

之前为了证明多项式*零知识*，我们使用了随机的$δ$位移，这带来了证明中的随机性（[零知识部分](https://medium.com/@imolfar/why-and-how-zk-snark-works-2-proving-knowledge-of-a-polynomial-f817760e2805#634e)）：
$$
\delta p(s)=t(s)·\delta h(s)
$$
通过计算，我们证明：
$$
L(s)·R(s)-O(s)=t(s)h(s)
$$
虽然我们可以将这种方法应用于使用相同*δ*的多个多项式，即提供随机值$δL ( s ) 、δR(s) 、δ^2O ( s ) 、 δ^2h(s)$，*这*将通过满足*有效运算的*配对检验：
$$
e(g,g)^{\delta^2L(s)R(s)}=e(g,g)^{\delta^2(t(s)h(s)+O(s))}
$$
问题是相同的$δ$会影响安全性，因为我们在证明中分别提供了这些值：

- 人们可以很容易地识别两个不同的多项式求值是否具有相同的价值，从而得到一些信息，例如：
	$$
	g^{\delta L(s)}=g^{\delta R(s)}
	$$

- $L(s)$ 和$R(s)$值之间潜在的细微差异可以通过暴力破解，例如，如果$L(s) = 5 R (s)$，迭代检验
	$$
	g^{L(s)}=(g^{R(S)})^i
	$$

因为$i\in\{1…N\}$，只需5 步就可以找到两者之间5倍的关系。同样可以对加密的加法运算进行暴力破解，例如，
$$
g^{L(s)}=g^{R(s)+5}
$$

- 多项式之间的其他相关性也会被发现，例如，如果
	$$
	e(g^{\delta L(s)},g^{\delta R(s)})=e(g^{\delta^2O(s)},g)
	$$

那么$L(x)⋅R(x)=O(x)$等等。

> 注意：[一致性检验优化](https://medium.com/@imolfar/why-and-how-zk-snark-works-6-verifiable-computation-protocol-1aa19f95a5cc#ea1f)使此类数据挖掘更加困难，除了验证者可以选择特定的ρₗ、 ρᵣ导致信息泄露（只要它不是去中心化的设置）的情况之外，仍然有发现关联性的可能。

因此，我们需要为每个多项式求值提供不同的随机性 ($δ$)，例如：
$$
\delta_lL(s)·\delta_rR(s)-\delta_oO(s)=t(s)·(\Delta\ ?\ h(s))
$$
为了解决等式右边的不相等性，在不修改的协议情况下我们倾向于，只能修改证明的值$h(s)$。此处的 Delta($\Delta$) 表示我们需要应用在$h(s)$上的差值，以平衡等式另一侧的随机性，而 ? 表示乘法或加法运算（这反过来也适用于除法和减法）。如果我们选择通过乘法 $(\ ? = ×)$ 来应用$\Delta$，这意味着在概率上不可能找到$\Delta$，因为随机性：
$$
\Delta=\frac{\delta_lL(s)·\delta_rR(s)-\delta_oO(s)}{t(s)h(s)}
$$
我们可以设置
$$
\delta_o=\delta_l·\delta_r
$$
则$\Delta$转化为：
$$
\Delta=\frac{\delta_l\delta_r(L(s)·R(s)-O(s))}{t(s)h(s)}=\delta_l\delta_r
$$
然而如前所述，这影响了零知识属性，更重要的是，这种构造将无法兼容验证者的输入多项式，因为它们也必须是相应$\delta$的倍数，这将需要交互。

我们可以尝试通过加法添加随机性：
$$
(L(s)+\delta_l)·(R(s)+\delta_r)-(O(s)+\delta_o)=t(s)·(\Delta\times h(s))
$$

$$
\Delta=\frac{\overbrace{L(s)R(s)-O(s)}^{t(s)h(s)}+\delta_rL(s)+\delta_lR(s)+\delta_l\delta_r-\delta_o}{t(s)h(s)}=1+\frac{\delta_rL(s)+\delta_lR(s)+\delta_l\delta_r-delta_o}{t(s)h(s)}
$$

但是由于随机性，它是无法整除的。即使我们通过将每个 $\delta$ 与$t(s)h(s)$相乘来解决这个问题，因为我们通过乘法以$h(s)$来应用$\Delta$，而$\Delta$由加密求值组成（即$E(L(s))$等等) ，在不使用配对的情况将无法计算（并且结果将会在另一个值域）
$$
g^{\Delta h(s)}
$$
同样地，使用$s$的加密次幂（从1到$d$次 ）对$\Delta h(x)$ 进行加密计算是不可能的，因为$h(x)$ 和$\Delta$ 的阶数是*d*，因此$\Delta h(x)$ 的阶数将会是至$2d$。除此之外，出于同样的原因，不可能计算如下的随机运算数多项式求值：
$$
g^{L(s)+\delta_l t(s)h(s)}
$$
因此，我们应该尝试通过加法$ ( ? = +)$ 来应用$\Delta$，因为它在同态加密值中是可行的。
$$
(L(s)+\delta_l)·(R(s)+\delta_r)-(O(s)+\delta_o)=t(s)·(\Delta+h(s))
$$

$$
\Delta=\frac{L(s)R(s)-O(s)+\delta_rL(s)+\delta_lR(s)+\delta_l\delta_r-\delta_o-t(s)h(s)}{t(s)}\Rightarrow \\
\Delta=\frac{\delta_rL(s)+\delta_lR(s)+\delta_l\delta_r-\delta_o}{t(s)}
$$

分子中的每一项都是$\delta$的倍数，因此我们可以通过将每个与$\delta$与$t(s)$相乘来使其整除：
$$
(L(s)+\delta_lt(s))·(R(s)+\delta_rt(s))-(O(s)+\delta_ot(s))=t(s)·(\Delta+h(s))\\
\cancel{L(s)R(s)-O(s)}+t(s)(\delta_rL(s)+\delta_lR(s)+\delta_l\delta_rt(s)-\delta_o)=t(s)\Delta+\cancel{t(s)h(s)}\\
\Delta=\delta_rL(s)+\delta_lR(s)+\delta_l\delta_rt(s)-\delta_o
$$
我们可以在加密空间中进行计算：
$$
g^{L(s)+\delta_lt(s)}=g^{L(s)}·{g^{t(s)}}^{\delta_l}
g^{\Delta}=(g^{L(s)})^{\delta_r}·(g^{R(s)})^{\delta_l}·(g^{t(s)})^{\delta_l\delta_r}g^{-\delta_o}
$$
这将在隐藏加密值的同时通过*有效运算检验。*
$$
L·R-O+{\color{magenta}t(\delta_rL+\delta_lR+\delta_l\delta_rt-\delta_o)}=t(s)h+{\color{magenta}t(s)(\delta_rL+\delta_lR+\delta_l\delta_rt-\delta_o)}
$$
由于对随机乘数$\delta_l,\delta_r,\delta_o$进行了一致的加法，该构造在统计上是*零知识*的（参考》 [Gen+12] 的定理 13）。

> 注意：这种做法也与验证者的运算数保持一致

$$
g_l^{L_p+\delta_lt}·g_l^{L_v}=g_l^{L_p+L_v+\delta_lt}
$$

> 因此，当且仅当证明者使用验证者的值来构建证明时（即$\Delta=\delta_r(L_p+L_v)+\delta_r(R_p+R_v)+\delta_l \delta_rt-\delta_o$，有效运算检验仍然成立，参考下一节的细节信息。

为了使“变量多项式约束”和“变量值一致性”检验与*零知识特性*一致，需要在证明密钥中添加如下参数：
$$
g_l^{t(s)},g_r^{t(s)},g_o^{t(s)},g_l^{\alpha_lt(s)},g_r^{\alpha_rt(s)},g_o^{\alpha_ot(s)},g_l^{\beta t(s)},g_r^{\beta t(s)},g_o^{\beta t(s)}
$$
有意思的是，最初的匹诺曹(Pinocchio)协议[Par+13]主要关注可验证计算，而较少关注*零知识*特性，这是一个很小的修改并且几乎是”免费的“。

# zk-SNARK 协议

结合所有逐步改进的点，最终的零知识简洁非交互式证明协议，又名匹诺曹Pinocchio [Par+13]协议如下（*零知识*组件是可选的，用*不同的颜色*进行了标识）：

- **设置**

	- 选择一个生成元$g$和加密配对$e$

	- 对于函数$f(u)=y$，共有$n$个变量，其中$m$个为输入/输出变量，转换成规模为$n+1$的阶数为$d$（等于运算步骤）的多项式形式(QAP)($\{l_i(x),r_i(x),o_i(x)\}_{i\in\{0,...,n\}},t(x)$)

	- 取样随机数$s,\rho_l,\rho_r,\alpha_l,\alpha_r,\alpha_o,\beta,\gamma$

	- 设置$\rho_o=\rho_l·\rho_r$，及对应的生成元$g_l=g^{\rho_l},g_r=g^{\rho_r},g_o=g^{\rho_o}$

	- 设置证明密钥
		$$
		(\{g^{s^k}\}_{k\in[d]}, \{g_l^{l_i(s)},g_r^{r_i(s)},g_o^{o_i(s)}\}_{i\in\{0,...,n\}},\\
		\{g_l^{\alpha_ll_i(s)},g_r^{\alpha_rr_i(s)},g_o^{\alpha_oo_i(s)},g_l^{\beta l_i(s)}g_r^{\beta r_i(s)}g_o^{\beta o_i(s)}\}_{i\in\{m+1,...,n\}},\\
		{\color{magenta}g_l^{t(s)},g_r^{t(s)},g_o^{t(s)},g_l^{\alpha_lt(s)},g_r^{\alpha_rt(s)},g_o^{\alpha_ot(s)},g_l^{\beta t(s)},g_r^{\beta t(s)},g_o^{\beta t(s)}}
		)
		$$

	- 设置验证密钥
		$$
		(g^1,g_o^{t(s)},\{g_l^{l_i(s)},g_r^{r_i(s)},g_o^{o_i(s)}\}_{i\in\{0,...,m\}},g^{\alpha_l},g^{\alpha_r},g^{\alpha_o},g^{\gamma},,g^{\gamma\beta})
		$$

- **证明**

	- 根据输入$u$, 计算 $y=f(u)$, 求得每一步运算中涉及的中间变量$\{v_i\}_{i\in\{m+1,...,n\}}$

	- 为所有未加密的变量多项式赋值$L(x)=l_0(x)+\sum_{i=1}^nv_i·l_i(x)$，同理计算R(x),O(x)$

	- $\color{magenta} 随机取样 \delta_l,\delta_r,\delta_o$

	- 计算$h(x)=\frac{L(x)R(x)-O(x)}{t(x)}+{\color{magenta}\delta_r L(x)+\delta_lR(x)+\delta_l\delta_rt(x)-\delta_o}$

	- 为加密后的变量多项式赋值，$\color{magenta}并应用\delta位移$，$g_l^{L_p(s)}={\color{magenta}(g_l^{t(s)})^{\delta_l}·}\displaystyle\prod_{i=m+1}^n(g_l^{l_i(s)})^{v_i}$，同理计算$g_r^{R_p(s)},g_o^{O_p(s)}$

	- 计算对应的$\alpha$位移，$g_l^{L^{'}_p(s)}={\color{magenta}(g_l^{\alpha_lt(s)})^{\delta_l}·}\displaystyle\prod_{i=m+1}^n(g_l^{\alpha_l l_i(s)})^{v_i}$，同理计算$g_r^{R^{'}_p(s)},g_o^{O^{'}_p(s)}$

	- 赋值变量一致性检验多项式
		$$
		g^{Z(s)}={\color{magenta}(g_l^{\beta t(s)})^{\delta_l}(g_r^{\beta t(s)})^{\delta_r}(g_o^{\beta t(s)})^{\delta_o}}·\displaystyle\prod_{i=m+1}^{n}(g_l^{\beta l_i(s)}g_r^{\beta r_i(s)}g_o^{\beta o_i(s)})^{v_i}
		$$

	- 计算证明$(g_l^{L_p(s)},g_r^{R_p(s)},g_o^{O_p(s)},g^{h(s)},g_l^{L^{'}_p(s)},g_r^{R^{'}_p(s)},g_o^{O^{'}_p(s)},g^{Z(s)})$

- **验证**

	- 解析证明为$(g_l^{L_p},g_r^{R_p},g_o^{O_p},g^{h},g_l^{L^{'}_p},g_r^{R^{'}_p},g_o^{O^{'}_p},g^{Z})$

	- 为证明者的加密后多项式赋值，并与1相加

		$g_l^{L_v(s)}=g_l^{l_0(s)}·\displaystyle\prod_{i=1}^m(g_l^{l_i(s)})^{v_i}$，同理计算$g_r^{R_v(s)},g_o^{O_v(s)}$

	- 变量多项式约束检验

		$e(g_l^{L_p},g^{\alpha_l})=e(g_l^{L_p^{'}},g)$，同理计算$g_r^{R_p},g_o^{O_p}$

	- 变量值一致性检验

		$e(g_l^{L_p}g_r^{R_p}g_o^{O_p},g^{\beta\gamma})=e(g^Z,g^{\gamma})$

	- 运算有效性检验

		$e(g_l^{L_p}g_l^{L_v(s)},g_r^{R_p}g_r^{R_v(s)})=e(g_o^{t(s)},g^h)·e(g_o^{O_p}g_o^{O_v(s)},g)$

	

# 结论

我们最终得到了一个有效的协议，它可以证明计算：

- 简洁地 — 与计算量无关，证明是恒定的大小
- 非交互式 — 一旦计算出证明，它就可以用来说服任意数量的验证者，而无需与证明者直接交互
- 有力的知识证明 — 声明毫无疑问是正确的，即伪造证明是不可行的；此外，证明者知道真实声明（即见证）的相应值，例如，如果该声明是“`B`是`sha256(a)`的结构”，那么证明者知道一些`a`满足`B = sha256(a)`，而`B`只能根据`a`的信息来计算，且无法通过`B`计算出`a`（假设`a`有熵足够大）
- *零知识的* — 从证明中提取任何知识是“十分困难的”，即它无法从随机性中提取出来

能实现这样的协议，主要归功于多项式的独特性质、模运算、同态加密、椭圆曲线密码学、密码学配对和发明者的创新性。

该协议证明了有限域上的计算的唯一性，几乎可以在一步运算中将任意数量的变量加在一起，但只能执行一次乘法。因此，存在着优化程序来有效利用这种特性的空间，并使用可以最大限度减少运算步骤的结构。

至关重要的是，验证者不必知道任何秘密值即可验证证明，以便任何人都可以以非交互的方式发布和使用正确构造的验证密钥。这与“指定验证者”的方案相反，在“指定验证者”的方案中，证明只能说服一方，因此它是不可转移的。

零知识证明领域仍在不断发展，引入了更多优化方案([BCTV13、Gro16、GM17]）和改进，例如可更新的证明和验证密钥([Gro+18])，以及新的构建方案(Bulletproofs [Bün+17]), ZK-STARK[Ben+18], Sonic [Mal+19])。



# 参考文献

[Gen+12] — Rosario Gennaro, Craig Gentry, Bryan Parno, and Mariana Raykova. *Quadratic* *Span Programs and Succinct NIZKs without PCPs*. Cryptology ePrint Archive, Report 2012/215. https://eprint.iacr.org/2012/215. 2012.

[Par+13] — Bryan Parno, Craig Gentry, Jon Howell, and Mariana Raykova. *Pinocchio: Nearly* *Practical Verifiable Computation*. Cryptology ePrint Archive, Report 2013/279. https://eprint.iacr.org/2013/279. 2013.

[BCTV13] — Eli Ben-Sasson, Alessandro Chiesa, Eran Tromer, Madars Virza. *Succinct Non-Interactive Zero Knowledge for a von Neumann Architecture*. Cryptology ePrint Archive, Report 2013/879. https://eprint.iacr.org/2013/879. 2013.

[Gro10] — Jens Groth. “Short pairing-based non-interactive zero-knowledge arguments”. In: *International Conference on the Theory and Application of Cryptology and* *Information Security*. Springer. 2010, pp. 321–340.

[GM17] — Jens Groth, Mary Maller. *Snarky Signatures: Minimal Signatures of Knowledge from Simulation-Extractable SNARKs*. Cryptology ePrint Archive, Report 2017/540. https://eprint.iacr.org/2017/540. 2017.

[Gro+18] — Jens Groth, Markulf Kohlweiss, Mary Maller, Sarah Meiklejohn, and Ian Miers. *Updatable and* *Universal Common Reference Strings with Applications to zk-SNARKs*. Cryptology ePrint Archive, Report 2018/280. https://eprint.iacr.org/2018/280. 2018.

[Bün+17] — Benedikt Bünz, Jonathan Bootle, Dan Boneh, Andrew Poelstra, Pieter Wuille, and Greg Maxwell. *Bulletproofs: Short* *Proofs for Confidential Transactions and More*. Cryptology ePrint Archive, Report 2017/1066. https://eprint.iacr.org/2017/1066. 2017.

[Ben+18] — Eli Ben-Sasson, Iddo Bentov, Yinon Horesh, and Michael Riabzev. *Scalable,* *transparent, and post-quantum secure computational integrity*. Cryptology ePrint Archive, Report 2018/046. https://eprint.iacr.org/2018/046. 2018.

[Mal+19] — Mary Maller, Sean Bowe, Markulf Kohlweiss, and Sarah Meiklejohn. *Sonic: Zero-Knowledge SNARKs from Linear-Size Universal* *and Updateable Structured Reference Strings*. Cryptology ePrint Archive, Report 2019/099. https://eprint.iacr.org/2019/099. 2019.
*原文：<Why and How zk-SNARK Works 7: Constraints and Public Inputs>*

*翻译：Junwei*

# 约束条件

我们的分析目前主要集中在运算的概念上。然而，该协议实际上并不是在“计算”，而是在检验输出值是否是运算数的正确运算结果。这就是为什么它被称为约束，即验证者正在约束证明者为预先定义的“程序”提供有效的计算值，无论它们是多少。多个约束的集合称为*约束系统*（在我们的例子中使用的是一阶约束系统或 R1CS）。

> 注意：这意味着找到所有正确解决方案的一种方法是对所有可能值的排列组合进行暴力破解，从中选出满足约束的值，或者使用更复杂技术的协议来满足约束 [ [con18](https://medium.com/@imolfar/why-and-how-zk-snark-works-7-constraints-and-public-inputs-e95f6596dd1c#b979) ]。

因此我们也可以使用约束来确保其他关系。例如，如果我们想确保变量a的值只能是 0 或 1（即二进制），我们可以使用如下的简单约束来实现：
$$
{\color{green}a}\times {\color{blue}a} ={\color{red}a}
$$
我们也可以约束*a*只能为2：
$$
{\color{green}a-2}\times {\color{blue}1} ={\color{red}0}
$$
一个更复杂的例子是确保数字*a*是一个 4 位数字（也称为半字节），换句话说，可以用 4 位表示a。我们也可以称其为“确保数字范围”，因为一个 4 位数字可以表示2⁴ 个组合，因此可以表示0～15范围内的16个数字。在十进制数字系统中，任何数字都可以表示为带相应的系数的底数为10的幂之和，例如，123 = 1 ⋅ 10² + 2⋅10¹ + 3⋅10⁰。类似地，二进制数可以表示为带相应系数的底数为2的幂之和，例如，1011（二进制）= 1⋅2³ + 0⋅2² + 1⋅2¹ + 1⋅2⁰ = 11（十进制）。

因此，如果*a*是 4 位数字，则可以表示用某些布尔值*b*₃, *b*₂, *b*₁, *b*₀来表示: *a* = *b*₃⋅2³ + *b*₂⋅2² + *b*₁⋅2¹ + *b*₀⋅2⁰。约束可以表示如下：
$$
1:\qquad{\color{green}a}\times {\color{blue}1} ={\color{red}8·b_3+4·b_2+2·b_1+1·b_0}
$$
为确保 *b*₃, *b*₂, *b*₁, *b*₀ 只能是二进制，我们需要添加：
$$
2:\qquad{\color{green}b_0}\times {\color{blue}b_0} ={\color{red}b_0}\\
3:\qquad{\color{green}b_1}\times {\color{blue}b_1} ={\color{red}b_1}\\
4:\qquad{\color{green}b_2}\times {\color{blue}b_2} ={\color{red}b_2}\\
5:\qquad{\color{green}b_3}\times {\color{blue}b_3} ={\color{red}b_3}
$$
可以通过这种方式应用相当复杂的约束，确保使用的值符合要求。重要的是要注意上述的约束1在当前运算的结构中是不可能实现的：
$$
{\color{green}\displaystyle\sum_{i=1}^n c_{l,i}·v_i}\times {\color{blue}\displaystyle\sum_{i=1}^n c_{r,i}·v_i} ={\color{red}\displaystyle\sum_{i=1}^n c_{o,i}·v_i}
$$
因为值 1（和前一个约束中的 2）必须表示为
$$
\color{blue} c·v_{one}
$$
其中*c*可以根植于证明密钥中，但*v*可能具有任何值，因为是证明者提供了它。虽然我们可以通过设置c = 0 来约束c ⋅*v_* one 为 0，但在我们受限的结构中很难找到强制v_ one等于1的约束。因此，验证者应该有一种方法来设置*v_one*的值。

# 公共输入和 1

如果无法根据验证者的输入检查证明，则证明的可用性将受到限制，例如，知道证明者已将两个值相乘但不知道结果和/或相乘的值是什么。虽然可以在证明密钥中“硬编码”要检验的值（例如，乘法的结果必须始终为 12），但这需要为每个所需的“验证者输入”生成单独的密钥对。

因此，如果验证者而不是证明者可以为计算指定一些值（输入或/和输出），包括*v_one*，，那将是通用的。

首先，让我们考虑证明值
$$
{\color{green}g^{L(s)}},{\color{blue}g^{R(s)}},{\color{red}g^{O(s)}}
$$
因为我们使用的是同态加密，所以可以累加这些值，例如，我们可以添加另一个加密的多项式求值
$$
g^{L(s)}·g^{l_{v(s)}}=g^{L(s)+l_v(s)}
$$
这意味着验证者可以将其他变量多项式添加到已经提供的多项式中。因此，如果我们可以从证明者可用的多项式中剔除必要的变量多项式，验证者就可以在这些变量上设置他的值，而计算检验应该仍然可以匹配。

这很容易实现，因为验证者已经在选择多项式时限制了证明者。因此，可以将这些可变多项式从证明密钥移动至验证密钥，同时剔除其对应的*α*-s位移和*β*校验和。

对协议进行必要的更新：

- **设置**

	- ...将所有$n$个变量多项式分为两组

		- 验证人的$m+1$个变量多项式

			$L_v(x)=l_0(x)+l_1(x)+...+l_m$，$R_v(x),O_v(x)$同理

			其中编号0为$v_{one}=1$预留

		- 证明者的$n-m$个变量多项式

			$L_p(x)=l_{m+1}(x)+...+l_n(x)$，

	- 设置证明密钥

		$(\{g^{s^k}\}_{k\in[d]},\{g_l^{l_i(s)},g_r^{r_i(s)},g_o^{o_i(s)},g_l^{\alpha_l l_i(s)},g_r^{\alpha_r r_i(s)},g_o^{\alpha_oo_i(s)},g_l^{\beta l_i(s)}·g_r^{\beta r_i(s)}·g_o^{\beta o_i(s)}\}_{i \in\{m+1,...,n\}})$

	- 添加至验证密钥

		$...,\{g_l^{l_i(s)},g_r^{r_i(s)},g_o^{o_i(s)}\}_{i\in\{0,...,m\}}$

- **证明**

	- ...计算包含验证者多项式在内的$h(x)$: $h(x)=\frac{L(x)·R(x)-O(x)}{t(x)}$,

		其中$L(x)=L_v(x)+L_p(x)$，$R(x),O(x)$同理

	- 提供证明

		$(g_l^{L_p(s)},g_r^{R_p(s)},g_o^{O_p(s)},g_l^{\alpha_l L_p(s)},g_r^{\alpha_r R_p(s)},g_o^{\alpha_oR_p(s)})$

- **验证**

	- 为验证人的变量多项式赋值，并加上1

		$g_l^{L_v(s)}=g_l^{l_0(s)}·\displaystyle\prod_{i=1}^{m}(g_l^{l_i(s)})^{v_i}$， $g_r^{R_v(s)},g_o^{O_v(s)}$同理

	- 变量多项式约束检验

		$e(g_l^{L_p},g^{\alpha_l})=e(g_l^{L^{'}_p},g)$， $g_r^{R_p},g_o^{O_p}$同理

	- 变量值一致性检验

		$e(g_l^{L_p}g_r^{R_p}g_o^{O_p},g^{\beta \gamma})=e(g^Z,g^{\gamma})$

	- 有效运算检验

		$e(g_l^{L_v(s)}g_l^{L_p(s)}, g_r^{R_v(s)}g_r^{R_p(s)})=e(g_o^t,g^h)·e(g_O^{O_v(s)}g_O^{O_p(s)},g)$

	

> 注意：根据协议属性（[单变量运算数多项式部分](https://medium.com/@imolfar/why-and-how-zk-snark-works-5-variable-polynomials-3b4e06859e30#8c18)），由多项式l*₀*(x), r*₀*(x), o*₀(x)表示的值1在相应的运算中已经具有相应的值，因此不需要赋值。
>
> 注意：验证者将不得不在验证步骤上承担额外的工作，这与他分配到的变量数量成正比。

实际上，这是将一些变量从证明者手中转移到验证者手中，同时仍然保持方程式的平衡。因此，*有效运算*检验应该仍然有效，但前提是证明者使用的值与验证者用于其输入的值相同。

值 1 是必不可少的，它允许通过乘以常数项（例如，将*a*乘以123）来得到任何数字（从给定的有限域中）：
$$
{\color{green}1·a}\times {\color{blue}123·v_{one}} ={\color{red}1·r}
$$

# 参考文献

[con18] — Wikipedia contributors. *Constraint satisfaction*. Wikipedia, The Free Encyclopedia. 2018.


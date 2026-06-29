# 学堂在线测试 —— 编译原理

## 高级程序设计语言的语法描述 习题

---

## 一、 单项选择题（本题共 10 小题，每小题 1 分，共 10 分）

**1. 文法 $G：S \to xS \mid y$ 所识别的语言是 ( C )。**

* A. $xyx$
* B. $(xyx)^*$
* C. $x^*y$
* D. $xy$

> **【解析】**
> 由 $S \to xS$ 可以不断在前面添加 $x$，最终由 $S \to y$ 结束推导。因此可以生成 $y, xy, xxy, xxxy, \ldots$，即 $x^*y$（零个或多个 $x$ 后跟一个 $y$）。

**2. 从编译程序的语法分析角度看，源程序是句子的集合，______ 可以较好地反映句子的结构。( B )**

* A. 线性表
* B. 树
* C. 强连通图
* D. 堆栈

> **【解析】**
> 语法分析的结果通常表示为语法树（分析树），树形结构能够自然地反映句子的层次结构和语法关系。

**3. 由文法的开始符号经 0 步或多步推导产生的文法符号序列是 ( C )**

* A. 短语
* B. 句柄
* C. 句型
* D. 句子

> **【解析】**
> 句型是由文法的开始符号出发，经过零步或多步推导得到的符号串（可以包含终结符和非终结符）。句子是不含非终结符的句型。

**4. 由文法的开始符号经 0 步或多步推导产生的不含非终结符号的文法符号序列是 ( D )**

* A. 短语
* B. 句柄
* C. 句型
* D. 句子

> **【解析】**
> 句子是句型的特例，要求推导结果中只包含终结符。即由开始符号推导得到的不含非终结符的符号串称为句子。

**5. 若文法 $G$ 是无二义的，则它的任何句子：( A )**

* A. 最左推导和最右推导对应的语法树必定相同
* B. 最左推导和最右推导对应的语法树可能不同
* C. 最左推导和最右推导必定相同
* D. 可能存在两个不同的最左推导，但它们对应的语法树相同

> **【解析】**
> 无二义文法的每个句子只有唯一的语法树。最左推导和最右推导虽然推导步骤的顺序不同，但它们对应的语法树是相同的（因为语法树唯一）。注意推导过程本身可以不同，但对应的树结构相同。

**6. 给定文法 $A \to bA \mid cc$，下面的符号串中为该文法句子的是 ( A )**
① $cc$  ② $bcbc$  ③ $bcbcc$  ④ $bccbcc$  ⑤ $bbbcc$

* A. ①⑤
* B. ①③④⑤
* C. ①④
* D. ①④⑤

> **【解析】**
> 该文法生成的语言为 $L = \{b^n cc \mid n \ge 0\}$。
>
> - ① $cc$：$n=0$，$A \Rightarrow cc$，符合 ✓
> - ② $bcbc$：不符合 $b^n cc$ 的形式 ✗
> - ③ $bcbcc$：不符合 $b^n cc$ 的形式（$b$ 和 $c$ 交替出现）✗
> - ④ $bccbcc$：不符合 $b^n cc$ 的形式（中间出现了 $cc$）✗
> - ⑤ $bbbcc$：$n=3$，$A \Rightarrow bA \Rightarrow bbA \Rightarrow bbbA \Rightarrow bbbcc$，符合 ✓

**7. 下列哪种文法是上下文无关文法的子集 ( D )**

* A. 0 型文法
* B. 1 型文法
* C. 2 型文法
* D. 3 型文法

> **【解析】**
> Chomsky 文法体系的包含关系为：0 型 ⊃ 1 型 ⊃ 2 型 ⊃ 3 型。上下文无关文法是 2 型文法，3 型文法（正规文法）是 2 型文法的真子集。

**8. 文法 $G$ 产生的 ( B ) 的全体称为该文法的语言。**

* A. 句型
* B. 句子
* C. 非终结符
* D. 终结符

> **【解析】**
> 文法 $G$ 的语言 $L(G)$ 定义为该文法产生的所有句子的集合，即由开始符号推导出的所有仅含终结符的符号串的集合。

**9. 若文法 $G$ 为：$S \to aS \mid b$，则该文法生成的语言是 ( A )。**

* A. 所有以 b 结尾的 a、b 字符串
* B. 所有含一个 b 和任意个 a 的字符串
* C. 所有以 a 开头、以 b 结尾的字符串
* D. 所有 a 的个数大于 b 的个数的字符串

> **【解析】**
> $L(G) = \{a^n b \mid n \ge 0\}$，即零个或多个 $a$ 后接一个 $b$。选项 A "所有以 b 结尾的 a、b 字符串" 最为贴切（注意这里字符串中只含 $a$ 和 $b$，且 $b$ 只出现在末尾，前面全是 $a$）。选项 B 错误，因为 $a$ 只能在 $b$ 之前；选项 C 错误，因为 $n$ 可以为 0（即只有 $b$）；选项 D 明显不符。

**10. 下列关于二义性文法的说法，错误的是 ( B )。**

* A. 二义性文法存在至少一个句子对应多棵语法树
* B. 二义性文法不能用于语法分析
* C. 可以通过增加约束规则（如运算符优先级）消除二义性
* D. 多数程序设计语言的文法本质上是二义性的，需通过附加规则处理

> **【解析】**
> B 选项说法错误。二义性文法可以通过附加消歧规则（如规定运算符优先级和结合性）来用于语法分析，实际的编程语言中经常这样做（例如 yacc/bison 中处理二义性文法）。二义性文法本身并非不能使用，只是需要额外的消歧规则。

---

## 二、 填空题（本题共 1 小题，每小题 1 分，共 1 分）

**1. 二义文法是指该文法存在一个句子 ______ **对应两棵或两棵以上不同的语法树（即存在两个不同的最左推导或最右推导）**。**

---

## 三、 主观题（本题共 6 小题，每小题 10 分，共 60 分）

**1. 设字母表 $\Sigma = \{a, b\}$，$U = \{ab, b\}$，$V = \{aa, bb\}$，求 $UV$, $\Sigma^*$, $\Sigma^+$。**

> **【参考答案】**
>
> - $UV = \{abaa, abbb, baa, bbb\}$
>   - $ab \cdot aa = abaa$
>   - $ab \cdot bb = abbb$
>   - $b \cdot aa = baa$
>   - $b \cdot bb = bbb$
> - $\Sigma^* = \{\varepsilon, a, b, aa, ab, ba, bb, aaa, aab, \ldots\}$，即 $\{a, b\}$ 上所有字符串的集合（包括空串 $\varepsilon$）。
> - $\Sigma^+ = \Sigma^* - \{\varepsilon\} = \{a, b, aa, ab, ba, bb, aaa, aab, \ldots\}$，即 $\{a, b\}$ 上所有非空字符串的集合。

**2. 已知文法 $G[S]$：**

$$
\begin{aligned}
S &\to a \mid \varepsilon \mid (T) \\
T &\to T, S \mid S
\end{aligned}
$$

**分别给出下列句子的最左和最右推导过程：**
**(1) $(a, (a, a))$**
**(2) $(a, (a, \varepsilon))$**

> **【参考答案】**
>
> **(1) $(a, (a, a))$**
>
> 最左推导：
>
> $$
> S \Rightarrow (T) \Rightarrow (T, S) \Rightarrow (S, S) \Rightarrow (a, S) \Rightarrow (a, (T)) \Rightarrow (a, (T, S)) \Rightarrow (a, (S, S)) \Rightarrow (a, (a, S)) \Rightarrow (a, (a, a))
> $$
>
> 最右推导：
>
> $$
> S \Rightarrow (T) \Rightarrow (T, S) \Rightarrow (T, (T)) \Rightarrow (T, (T, S)) \Rightarrow (T, (T, a)) \Rightarrow (T, (S, a)) \Rightarrow (T, (a, a)) \Rightarrow (S, (a, a)) \Rightarrow (a, (a, a))
> $$
>
> **(2) $(a, (a, \varepsilon))$**
>
> 最左推导：
>
> $$
> S \Rightarrow (T) \Rightarrow (T, S) \Rightarrow (S, S) \Rightarrow (a, S) \Rightarrow (a, (T)) \Rightarrow (a, (T, S)) \Rightarrow (a, (S, S)) \Rightarrow (a, (a, S)) \Rightarrow (a, (a, \varepsilon))
> $$
>
> 最右推导：
>
> $$
> S \Rightarrow (T) \Rightarrow (T, S) \Rightarrow (T, (T)) \Rightarrow (T, (T, S)) \Rightarrow (T, (T, \varepsilon)) \Rightarrow (T, (S, \varepsilon)) \Rightarrow (T, (a, \varepsilon)) \Rightarrow (S, (a, \varepsilon)) \Rightarrow (a, (a, \varepsilon))
> $$

**3. 考虑文法 $G[S]$：**

$$
\begin{aligned}
S &\to bA \\
A &\to aA \mid a
\end{aligned}
$$

**该文法定义了一个什么样的语言？**

> **【参考答案】**
> $L(G) = \{ba^n \mid n \ge 1\}$
>
> 即所有以一个 $b$ 开头、后跟一个或多个 $a$ 的字符串集合。
>
> 分析：$S \to bA$ 产生一个前导 $b$；$A \to aA \mid a$ 可以生成一个或多个 $a$。因此该语言为 $\{ba, baa, baaa, baaaa, \ldots\}$。

**4. 构造一个文法 $G$，使 $L(G) = \{a^n b^n \mid n \ge 1\}$。**

> **【参考答案】**
>
> $$
> G[S]: \quad S \to aSb \mid ab
> $$
>
> 验证：
>
> - $n = 1$：$S \Rightarrow ab$ ✓
> - $n = 2$：$S \Rightarrow aSb \Rightarrow aabb$ ✓
> - $n = 3$：$S \Rightarrow aSb \Rightarrow aaSbb \Rightarrow aaabbb$ ✓
>
> 每次使用 $S \to aSb$ 在两端分别添加一个 $a$ 和一个 $b$，最终用 $S \to ab$ 终止递归，保证 $a$ 和 $b$ 的数量相等且 $n \ge 1$。

**5. 给定文法 $G[E]$：**

$$
\begin{aligned}
E &\to E i T \mid T \\
T &\to T + F \mid i F \mid F \\
F &\to E * \mid (
\end{aligned}
$$

**请回答该文法是否为二义文法，说明理由。**

> **【参考答案】**
> 该文法是**二义文法**。
>
> **理由**：若一个文法存在某个句子，该句子有两棵或两棵以上不同的语法树（或两个不同的最左推导/最右推导），则该文法是二义文法。
>
> 对于该文法，我们能找到多个具有两棵不同语法树的句子：
>
> ---
>
> ### 示例一：句子 $i(\ast$
>
> 该句子存在两个不同的最左推导：
>
> - **最左推导 1**：
>   $$
>   E \Rightarrow T \Rightarrow F \Rightarrow E\ast \Rightarrow T\ast \Rightarrow iF\ast \Rightarrow i(\ast
>   $$
>
> - **最左推导 2**：
>   $$
>   E \Rightarrow T \Rightarrow iF \Rightarrow iE\ast \Rightarrow iT\ast \Rightarrow iF\ast \Rightarrow i(\ast
>   $$
>
> 对应的两棵语法树结构不同（第一棵树中，$\ast$ 是在最外层的 $F \to E\ast$ 中引入的；而第二棵树中，$\ast$ 是在 $T \to iF \to iE\ast$ 中引入的）。
>
> ---
>
> ### 示例二：句子 $i( + (\ast$
>
> 该句子也存在两个不同的最左推导，对应不同的结合方式：
>
> - **最左推导 1**（将 $+$ 作为最外层算符）：
>   $$
>   E \Rightarrow T \Rightarrow T + F \Rightarrow iF + F \Rightarrow i( + F \Rightarrow i( + E\ast \Rightarrow i( + T\ast \Rightarrow i( + F\ast \Rightarrow i( + (\ast
>   $$
>
> - **最左推导 2**（将 $\ast$ 作为最外层算符）：
>   $$
>   E \Rightarrow T \Rightarrow iF \Rightarrow iE\ast \Rightarrow i(E i T)\ast \Rightarrow i(T i T)\ast \Rightarrow i(F i T)\ast \Rightarrow i(( i T)\ast \Rightarrow i(( i F)\ast \Rightarrow i(( i (\ast
>   $$
>
> （注：在最左推导 2 中，由于 $E \Rightarrow E i T$，我们可以将 $i$ 解释为 $E \to E i T$ 产生式中的中间终结符，从而把整个表达式包裹在 $\ast$ 运算符内。这与最左推导 1 中直接由 $+$ 联结两个部分的结构不同，因此对应两棵不同的语法树。）
>
> 由于对上述句子都可以构造出两棵不同的语法树，因此该文法是二义文法。

**6. 令文法 $G_6$ 为：**

$$
\begin{aligned}
N &\to D \mid ND \\
D &\to 0 \mid 1 \mid 2 \mid 3 \mid 4 \mid 5 \mid 6 \mid 7 \mid 8 \mid 9
\end{aligned}
$$

**(1) $G_6$ 的语言 $L(G_6)$ 是什么？**
**(2) 给出句子 `0127`、`34` 和 `568` 的最左推导和最右推导。**

> **【参考答案】**
>
> **(1)** $L(G_6)$ 是所有由一个或多个十进制数字组成的字符串的集合，即所有非空十进制数字串。
>
> $$
> L(G_6) = \{d_1 d_2 \cdots d_n \mid n \ge 1, \; d_i \in \{0, 1, 2, \ldots, 9\}\}
> $$
>
> **(2)** 最左推导和最右推导如下：
>
> **句子 `0127`：**
>
> 最左推导：
>
> $$
> N \Rightarrow ND \Rightarrow NDD \Rightarrow NDDD \Rightarrow DDDD \Rightarrow 0DDD \Rightarrow 01DD \Rightarrow 012D \Rightarrow 0127
> $$
>
> 最右推导：
>
> $$
> N \Rightarrow ND \Rightarrow N7 \Rightarrow ND7 \Rightarrow N27 \Rightarrow ND27 \Rightarrow N127 \Rightarrow D127 \Rightarrow 0127
> $$
>
> **句子 `34`：**
>
> 最左推导：
>
> $$
> N \Rightarrow ND \Rightarrow DD \Rightarrow 3D \Rightarrow 34
> $$
>
> 最右推导：
>
> $$
> N \Rightarrow ND \Rightarrow N4 \Rightarrow D4 \Rightarrow 34
> $$
>
> **句子 `568`：**
>
> 最左推导：
>
> $$
> N \Rightarrow ND \Rightarrow NDD \Rightarrow DDD \Rightarrow 5DD \Rightarrow 56D \Rightarrow 568
> $$
>
> 最右推导：
>
> $$
> N \Rightarrow ND \Rightarrow N8 \Rightarrow ND8 \Rightarrow N68 \Rightarrow D68 \Rightarrow 568
> $$

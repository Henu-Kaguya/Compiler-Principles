# 学堂在线测试 —— 编译原理

## 语法分析----自上而下分析 习题

---

## 一、 单项选择题（本题共 15 小题，每小题 1 分，共 15 分）

**1. 编译过程中，语法分析器的任务是 ( B )。**
① 分析单词是怎样构成的
② 分析单词串是如何构成语句和说明的
③ 分析语句和说明是如何构成程序的
④ 分析程序的结构

* A. ②③
* B. ②③④
* C. ①②③
* D. ①②③④

> **【解析】**
> 语法分析器的任务是在词法分析的基础上，根据文法规则分析单词串如何构成语句和说明（②），分析语句和说明如何构成程序（③），以及分析程序的整体结构（④）。①"分析单词是怎样构成的"是**词法分析**的任务，不属于语法分析。因此选 B。

**2. 在高级语言编译程序常用的语法分析方法中，预测分析方法属于 ( B )。**

* A. 自左至右分析法
* B. 自上而下分析法
* C. 自下而上分析法
* D. 自右至左分析法

> **【解析】**
> 预测分析法（Predictive Parsing）是一种不带回溯的递归下降分析方法，属于自上而下（Top-Down）分析法。它从文法的开始符号出发，根据当前输入符号预测使用哪个产生式，逐步推导出输入串。

**3. 关于 LL(1) 文法，以下说法正确的是 ( A )。**

* A. 使用 LL(1) 文法能够进行有效的自上而下语法分析
* B. 使用 LL(1) 文法能够进行有效的自下而上语法分析
* C. LL(1) 文法可以含有左递归
* D. 任何上下文无关文法都一定是 LL(1) 的

> **【解析】**
> LL(1) 文法是专为自上而下分析设计的文法类。LL(1) 文法**不能含有左递归**（否则会导致无限循环），C 错误；并非所有上下文无关文法都是 LL(1) 的，D 错误；LL(1) 是自上而下分析的文法，B 的说法不准确。A 正确。

**4. 下列哪项不属于语法分析的方法 ( C )。**

* A. 递归下降分析法
* B. LR 分析法
* C. 乔姆斯基范式分析法
* D. 算符优先分析法

> **【解析】**
> 递归下降分析法（自上而下）、LR 分析法（自下而上）、算符优先分析法（自下而上）都是常用的语法分析方法。乔姆斯基范式（Chomsky Normal Form, CNF）是一种文法的标准化形式，不是一种语法分析方法。

**5. 自顶向下语法分析中，避免回溯的关键是 ( D )。**

* A. 采用 LL(1) 文法
* B. 消除左递归
* C. 提取左因子
* D. 以上都是

> **【解析】**
> 自顶向下分析中，要避免回溯需要综合多种措施：采用 LL(1) 文法确保分析的确定性，消除左递归避免无限循环，提取左因子消除相同前缀带来的不确定性。三者缺一不可，因此选 D。

**6. 下列哪种方法不属于自顶向下的语法分析方法 ( C )。**

* A. 递归下降分析法
* B. LL(1) 分析法
* C. SLR(1) 分析法
* D. 预测分析法

> **【解析】**
> 递归下降分析法、LL(1) 分析法和预测分析法都属于自上而下的语法分析方法。SLR(1)（Simple LR）分析法属于**自下而上**的 LR 分析法家族。

**7. LL(1) 文法中的 "1" 表示 ( C )。**

* A. 分析过程中每次回溯 1 次
* B. 文法是 1 型文法（上下文有关文法）
* C. 分析时每次向前看 1 个输入符号
* D. 产生式的右部长度不超过 1

> **【解析】**
> LL(1) 中第一个 L 表示从左到右扫描输入，第二个 L 表示最左推导，括号中的 "1" 表示每次向前看（lookahead）1 个输入符号来决定使用哪个产生式。

**8. 下列关于左递归文法的说法，正确的是 ( B )。**

* A. 左递归文法可以直接用于 LL(1) 分析
* B. 左递归是指产生式左部符号在右部开头出现（如 $A \to A\alpha$）
* C. 所有左递归文法都无法进行语法分析
* D. 左递归只会出现在上下文无关文法中

> **【解析】**
> 左递归是指非终结符 $A$ 的产生式右部以 $A$ 自身开头（直接左递归 $A \to A\alpha$）。左递归文法不能直接用于 LL(1) 分析（A 错），但可以通过自下而上方法分析（C 错）。左递归并非上下文无关文法独有（D 错）。B 是正确的定义。

**9. 下列哪种文法可能存在二义性 ( A )。**

* A. 一个句子对应两棵不同的语法树
* B. 文法中存在左递归
* C. 文法中存在 $\varepsilon$ 产生式
* D. 文法是 LL(1) 文法

> **【解析】**
> 二义性的定义是：如果一个文法中存在某个句子，它有两棵（或以上）不同的语法树（即两个不同的最左推导或最右推导），则该文法是二义的。左递归、$\varepsilon$ 产生式与二义性没有必然联系；LL(1) 文法一定是无二义的。

**10. 在 LL(1) 分析中，若对于非终结符 $A$ 和输入符号 $a$，有多个产生式 $A \to \alpha$ 都满足 $\text{FIRST}(\alpha)$ 包含 $a$，则该文法 ( C )。**

* A. 是 LL(1) 文法
* B. 存在左递归
* C. 存在回溯风险，不符合 LL(1) 条件
* D. 可以直接用于递归下降分析

> **【解析】**
> LL(1) 文法要求对同一非终结符的不同产生式，其 FIRST 集两两不相交。若多个产生式的 FIRST 集都包含同一终结符 $a$，则分析器无法确定选用哪个产生式，存在回溯风险，不满足 LL(1) 条件。

**11. 编译程序的各个阶段中，______ 阶段的输出是语法树。**

* A. 词法分析
* B. 语法分析
* C. 语义分析
* D. 中间代码生成

> **【解析】**
> 语法分析阶段以词法分析输出的单词符号串（Token 序列）为输入，根据文法规则进行分析，输出语法树（Parse Tree / Syntax Tree）。

**12. 给定产生式 $A \to \alpha B \beta$，计算 $\text{FIRST}(\alpha \beta)$ 时，以下哪项是正确的？ ( A )**

* A. 如果 $\alpha$ 不能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha \beta) = \text{FIRST}(\alpha)$
* B. 如果 $\alpha$ 能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha \beta) = (\text{FIRST}(\alpha) \setminus \{\varepsilon\}) \cup \text{FIRST}(\beta)$
* C. 无论 $\alpha$ 能否推导出 $\varepsilon$，$\text{FIRST}(\alpha \beta)$ 都等于 $\text{FIRST}(\alpha)$
* D. 如果 $\alpha$ 能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha \beta) = \text{FIRST}(\beta)$

> **【解析】**
> 计算 $\text{FIRST}(\alpha \beta)$ 的规则：若 $\alpha$ 不能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha\beta) = \text{FIRST}(\alpha)$，A 正确。若 $\alpha$ 能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha\beta) = (\text{FIRST}(\alpha) \setminus \{\varepsilon\}) \cup \text{FIRST}(\beta)$（B 的描述在 $\beta$ 也可能推导出 $\varepsilon$ 时不够完整，需要进一步考虑 $\beta$ 的情况）。C 和 D 明显错误。A 的条件和结论完全正确。

**13. 已知文法 $G$：**

$$
\begin{aligned}
S &\to Aa \mid b \\
A &\to Sc \mid d
\end{aligned}
$$

**该文法属于 ( B )。**

* A. 直接左递归
* B. 间接左递归
* C. 无左递归
* D. 既是直接左递归也是间接左递归

> **【解析】**
> 文法中没有直接左递归（没有 $S \to S\dots$ 或 $A \to A\dots$ 的产生式）。但存在间接左递归：$S \Rightarrow Aa \Rightarrow Sca$，即 $S$ 经过两步推导后又回到了以 $S$ 开头的句型，构成间接左递归。

**14. 若文法 $G$ 经消除左递归后得到文法 $G'$，则下列说法正确的是 ( B )。**

* A. $G$ 和 $G'$ 的终结符集不同
* B. $G$ 和 $G'$ 产生的语言完全相同
* C. $G$ 和 $G'$ 的非终结符集相同
* D. $G'$ 一定是 LL(1) 文法

> **【解析】**
> 消除左递归是一种等价变换，变换后文法产生的语言不变（B 正确）。消除左递归时通常引入新的非终结符（如 $A'$），因此非终结符集会改变（C 错）；终结符集不变（A 错）；消除左递归后不一定就是 LL(1) 文法，还可能需要提取左因子等操作（D 错）。

**15. 递归下降分析法无法处理含左递归的文法，其根本原因是 ( B )。**

* A. 左递归会导致文法二义性
* B. 左递归会使递归调用陷入无限循环
* C. 左递归会增加语法分析的时间复杂度
* D. 左递归会减少产生式的数量

> **【解析】**
> 递归下降分析法为每个非终结符编写一个递归函数。若文法含左递归（如 $A \to A\alpha$），则分析 $A$ 时会立即再次调用 $A$ 的分析函数，且未消耗任何输入符号，导致无限递归调用。

---

## 二、 多项选择题（本题共 2 小题，每小题 2 分，共 4 分。多选、少选、错选均不得分）

**1. 计算非终结符 $A$ 的 $\text{FOLLOW}$ 集时，考虑产生式 $B \to \alpha A \beta$，以下哪项需要加入 $\text{FOLLOW}(A)$？ ( A, B, D )**

* A. $\text{FIRST}(\beta)$
* B. 如果 $\beta$ 能推导出 $\varepsilon$，则还要加入 $\text{FOLLOW}(B)$
* C. $\text{FIRST}(\beta)$ 和 $\text{FOLLOW}(B)$
* D. 如果 $\beta$ 不能推导出 $\varepsilon$，则加入 $\text{FIRST}(\beta)$；如果 $\beta$ 能推导出 $\varepsilon$，则加入 $(\text{FIRST}(\beta) \setminus \{\varepsilon\}) \cup \text{FOLLOW}(B)$

> **【解析】**
> 对于产生式 $B \to \alpha A \beta$，FOLLOW(A) 的计算规则如下：
> - 将 $\text{FIRST}(\beta) \setminus \{\varepsilon\}$ 加入 $\text{FOLLOW}(A)$（A 部分正确，严格说应去掉 $\varepsilon$）；
> - 若 $\beta \Rightarrow^* \varepsilon$，则还要将 $\text{FOLLOW}(B)$ 加入 $\text{FOLLOW}(A)$（B 正确）；
> - D 给出了最完整、最精确的描述（D 正确）；
> - C 说无条件加入 $\text{FOLLOW}(B)$，这是错误的，只有 $\beta$ 能推导出 $\varepsilon$ 时才加入。

**2. 已知文法 $G[A]$： ( C, D )**

$$
\begin{aligned}
A &\to aB \mid aC \\
B &\to b \\
C &\to c
\end{aligned}
$$

**该文法是：**

* A. LL(1) 文法
* B. 非 LL(1) 文法，因为它存在左递归
* C. 非 LL(1) 文法，因为它存在公共左因子（$A \to aB$ 和 $A \to aC$ 都以 $a$ 开头）
* D. 非 LL(1) 文法，因为它需要回溯

> **【解析】**
> 产生式 $A \to aB$ 和 $A \to aC$ 具有公共左因子 $a$，即 $\text{FIRST}(aB) \cap \text{FIRST}(aC) = \{a\} \neq \emptyset$，不满足 LL(1) 条件（C 正确）。因为存在公共左因子，分析器在看到输入 $a$ 时无法确定选择哪个产生式，需要回溯（D 正确）。该文法不存在左递归（B 错误），也不是 LL(1) 文法（A 错误）。

---

## 三、 判断题（本题共 3 小题，每小题 1 分，共 3 分）

**1. 每个文法都能改写为 LL(1) 文法。** ( × )

> **【解析】**
> 并非每个上下文无关文法都能改写为 LL(1) 文法。有些固有二义性文法或某些非 LL 语言的文法无法通过消除左递归、提取左因子等手段转换为 LL(1) 文法。

**2. 一个 LL(1) 文法一定是无二义的。** ( √ )

> **【解析】**
> LL(1) 文法要求对每个非终结符和每个输入符号，最多只能选择一个产生式，因此分析过程是确定性的，不可能产生两棵不同的语法树。所以 LL(1) 文法一定是无二义的。

**3. 欲构造行之有效的自上而下分析器，则只需消除左递归。** ( × )

> **【解析】**
> 构造有效的自上而下分析器，仅消除左递归是不够的。还需要进行**提取左因子**等处理，使文法满足 LL(1) 条件（即各产生式的 FIRST 集不相交等），才能保证分析过程无回溯、高效确定。

---

## 四、 填空题（本题共 2 小题，每小题 2 分，共 4 分）

**1. 语法分析最常用的两类方法是 ______ **自上而下** 和 ______ **自下而上** 分析法。**

**2. 语法分析器的输入是 ______ **单词符号串（Token 序列）**，其输出是 ______ **语法树**。**

---

## 五、 主观题（本题共 2 小题，每小题 10 分，共 20 分）

**1. 下面文法中哪些是 LL(1) 的，说明理由。**

**①**

$$
\begin{aligned}
S &\to Abc \\
A &\to a \mid \varepsilon \\
B &\to b \mid \varepsilon
\end{aligned}
$$

**②**

$$
\begin{aligned}
S &\to ABBA \\
A &\to a \mid \varepsilon \\
B &\to b \mid \varepsilon
\end{aligned}
$$

**③**

$$
\begin{aligned}
S &\to Ab \\
A &\to a \mid B \mid \varepsilon \\
B &\to b \mid \varepsilon
\end{aligned}
$$

**④**

$$
\begin{aligned}
S &\to aSe \mid B \\
B &\to bBe \mid C \\
C &\to cCe \mid d
\end{aligned}
$$

> **【参考答案】**
>
> ---
>
> **① 是 LL(1) 文法。**
>
> 计算 FIRST 集和 FOLLOW 集：
>
> | 非终结符 | FIRST | FOLLOW |
> |---------|-------|--------|
> | $S$ | $\{a, b, c\}$ | $\{\$\}$ |
> | $A$ | $\{a, \varepsilon\}$ | $\{b, c\}$ |
> | $B$ | $\{b, \varepsilon\}$ | $\{c\}$ |
>
> 验证 LL(1) 条件：
> - $A \to a \mid \varepsilon$：$\text{FIRST}(a) \cap (\text{FIRST}(\varepsilon) \cup \text{FOLLOW}(A)) = \{a\} \cap \{b, c\} = \emptyset$ ✓
> - $B \to b \mid \varepsilon$：$\text{FIRST}(b) \cap (\text{FIRST}(\varepsilon) \cup \text{FOLLOW}(B)) = \{b\} \cap \{c\} = \emptyset$ ✓
>
> 所有条件满足，**是 LL(1) 文法**。
>
> ---
>
> **② 不是 LL(1) 文法。**
>
> 计算 FIRST 集和 FOLLOW 集：
>
> | 非终结符 | FIRST | FOLLOW |
> |---------|-------|--------|
> | $S$ | $\{a, b, \varepsilon\}$ | $\{\$\}$ |
> | $A$ | $\{a, \varepsilon\}$ | $\{a, b, \$\}$ |
> | $B$ | $\{b, \varepsilon\}$ | $\{a, b, \$\}$ |
>
> 产生式 $S \to ABBA$：$S$ 只有一个产生式，无需检查。
>
> 验证 LL(1) 条件：
> - $A \to a \mid \varepsilon$：$\text{FIRST}(a) \cap \text{FOLLOW}(A) = \{a\} \cap \{a, b, \$\} = \{a\} \neq \emptyset$ ✗
>
> $A$ 的两个候选式不满足 LL(1) 条件，**不是 LL(1) 文法**。
>
> 直觉上，当输入为 $a$ 时，无法确定应该由哪个 $A$ 或 $B$ 来匹配，因为所有非终结符都可以推导出 $\varepsilon$。
>
> ---
>
> **③ 不是 LL(1) 文法。**
>
> 计算 FIRST 集和 FOLLOW 集：
>
> | 非终结符 | FIRST | FOLLOW |
> |---------|-------|--------|
> | $S$ | $\{a, b\}$ | $\{\$\}$ |
> | $A$ | $\{a, b, \varepsilon\}$ | $\{b\}$ |
> | $B$ | $\{b, \varepsilon\}$ | $\{b\}$ |
>
> 验证 LL(1) 条件：
> - $A \to a \mid B \mid \varepsilon$：
>   - $\text{FIRST}(B) = \{b, \varepsilon\}$，由于 $B$ 可推导出 $\varepsilon$，需考虑 $\text{FOLLOW}(A) = \{b\}$
>   - 对于候选式 $B$ 的预测集：$(\text{FIRST}(B) \setminus \{\varepsilon\}) \cup \text{FOLLOW}(A) = \{b\} \cup \{b\} = \{b\}$
>   - 对于候选式 $\varepsilon$ 的预测集：$\text{FOLLOW}(A) = \{b\}$
>   - $\{b\} \cap \{b\} = \{b\} \neq \emptyset$ ✗
>
> $A$ 的候选式 $B$ 和 $\varepsilon$ 的预测集有交集，**不是 LL(1) 文法**。
>
> ---
>
> **④ 是 LL(1) 文法。**
>
> 计算 FIRST 集和 FOLLOW 集：
>
> | 非终结符 | FIRST | FOLLOW |
> |---------|-------|--------|
> | $S$ | $\{a, b, c, d\}$ | $\{\$, e\}$ |
> | $B$ | $\{b, c, d\}$ | $\{\$, e\}$ |
> | $C$ | $\{c, d\}$ | $\{\$, e\}$ |
>
> 验证 LL(1) 条件：
> - $S \to aSe \mid B$：$\text{FIRST}(aSe) \cap \text{FIRST}(B) = \{a\} \cap \{b, c, d\} = \emptyset$ ✓
> - $B \to bBe \mid C$：$\text{FIRST}(bBe) \cap \text{FIRST}(C) = \{b\} \cap \{c, d\} = \emptyset$ ✓
> - $C \to cCe \mid d$：$\text{FIRST}(cCe) \cap \text{FIRST}(d) = \{c\} \cap \{d\} = \emptyset$ ✓
>
> 所有非终结符的候选式 FIRST 集两两不相交，且无 $\varepsilon$ 产生式，**是 LL(1) 文法**。

**2. 已知文法 $G[S]$：**

$$
\begin{aligned}
S &\to (L) \mid aS \mid a \\
L &\to L, S \mid S
\end{aligned}
$$

**(1) 消除左递归和回溯；**
**(2) 计算每个非终结符的 $\text{First}$ 和 $\text{Follow}$ 集；**
**(3) 构造预测分析表。**

> **【参考答案】**
>
> ---
>
> **(1) 消除左递归和回溯**
>
> **第一步：提取左因子**
>
> $S \to aS \mid a$ 有公共左因子 $a$，提取左因子：
>
> $$S \to (L) \mid aS'$$
> $$S' \to S \mid \varepsilon$$
>
> **第二步：消除左递归**
>
> $L \to L, S \mid S$ 存在直接左递归，消除：
>
> $$L \to SL'$$
> $$L' \to , SL' \mid \varepsilon$$
>
> **变换后的文法 $G'[S]$：**
>
> $$
> \begin{aligned}
> S &\to (L) \mid aS' \\
> S' &\to S \mid \varepsilon \\
> L &\to SL' \\
> L' &\to ,\;SL' \mid \varepsilon
> \end{aligned}
> $$
>
> ---
>
> **(2) 计算 FIRST 集和 FOLLOW 集**
>
> **FIRST 集：**
>
> | 非终结符 | FIRST 集 |
> |---------|---------|
> | $S$ | $\{(,\; a\}$ |
> | $S'$ | $\{(,\; a,\; \varepsilon\}$ |
> | $L$ | $\{(,\; a\}$ |
> | $L'$ | $\{,,\; \varepsilon\}$ |
>
> 计算过程：
> - $\text{FIRST}(S)$：由 $S \to (L)$ 得 $($ ；由 $S \to aS'$ 得 $a$。故 $\text{FIRST}(S) = \{(, a\}$。
> - $\text{FIRST}(S')$：由 $S' \to S$ 得 $\text{FIRST}(S) = \{(, a\}$；由 $S' \to \varepsilon$ 得 $\varepsilon$。故 $\text{FIRST}(S') = \{(, a, \varepsilon\}$。
> - $\text{FIRST}(L)$：由 $L \to SL'$ 得 $\text{FIRST}(S) = \{(, a\}$。故 $\text{FIRST}(L) = \{(, a\}$。
> - $\text{FIRST}(L')$：由 $L' \to ,\;SL'$ 得 $,$；由 $L' \to \varepsilon$ 得 $\varepsilon$。故 $\text{FIRST}(L') = \{,, \varepsilon\}$。
>
> **FOLLOW 集：**
>
> | 非终结符 | FOLLOW 集 |
> |---------|----------|
> | $S$ | $\{\$,\; ,,\; )\}$ |
> | $S'$ | $\{\$,\; ,,\; )\}$ |
> | $L$ | $\{)\}$ |
> | $L'$ | $\{)\}$ |
>
> 计算过程：
> - $\text{FOLLOW}(S)$：$S$ 是开始符号，加入 $\$$。由 $L \to SL'$，将 $\text{FIRST}(L') \setminus \{\varepsilon\} = \{,\}$ 加入；又因 $L' \Rightarrow^* \varepsilon$，将 $\text{FOLLOW}(L) = \{)\}$ 加入。由 $L' \to ,\;SL'$，同理加入 $\{,\}$ 和 $\{)\}$。由 $S' \to S$，将 $\text{FOLLOW}(S')$ 加入。故 $\text{FOLLOW}(S) = \{\$, ,, )\}$。
> - $\text{FOLLOW}(S')$：由 $S \to aS'$，将 $\text{FOLLOW}(S)$ 加入。故 $\text{FOLLOW}(S') = \{\$, ,, )\}$。
> - $\text{FOLLOW}(L)$：由 $S \to (L)$，将 $)$ 加入。故 $\text{FOLLOW}(L) = \{)\}$。
> - $\text{FOLLOW}(L')$：由 $L \to SL'$，将 $\text{FOLLOW}(L) = \{)\}$ 加入。由 $L' \to ,\;SL'$，将 $\text{FOLLOW}(L') $ 加入（自身，已包含）。故 $\text{FOLLOW}(L') = \{)\}$。
>
> ---
>
> **(3) 构造预测分析表**
>
> 对每条产生式，根据 FIRST 集和 FOLLOW 集确定表项：
>
> | 非终结符 | $($ | $a$ | $,$ | $)$ | $\$$ |
> |---------|-----|-----|-----|-----|------|
> | $S$ | $S \to (L)$ | $S \to aS'$ | | | |
> | $S'$ | $S' \to S$ | $S' \to S$ | $S' \to \varepsilon$ | $S' \to \varepsilon$ | $S' \to \varepsilon$ |
> | $L$ | $L \to SL'$ | $L \to SL'$ | | | |
> | $L'$ | | | $L' \to ,\;SL'$ | $L' \to \varepsilon$ | |
>
> 填表依据：
> - $S \to (L)$：$\text{FIRST}((L)) = \{(\}$，填入 $M[S, (]$
> - $S \to aS'$：$\text{FIRST}(aS') = \{a\}$，填入 $M[S, a]$
> - $S' \to S$：$\text{FIRST}(S) = \{(, a\}$，填入 $M[S', (]$ 和 $M[S', a]$
> - $S' \to \varepsilon$：$\text{FOLLOW}(S') = \{\$, ,, )\}$，填入 $M[S', \$]$、$M[S', ,]$、$M[S', )]$
> - $L \to SL'$：$\text{FIRST}(S) = \{(, a\}$，填入 $M[L, (]$ 和 $M[L, a]$
> - $L' \to ,\;SL'$：$\text{FIRST}(,\;SL') = \{,\}$，填入 $M[L', ,]$
> - $L' \to \varepsilon$：$\text{FOLLOW}(L') = \{)\}$，填入 $M[L', )]$
>
> 分析表中没有多重定义的表项，因此变换后的文法是 **LL(1) 文法**，可以进行确定的自上而下分析。

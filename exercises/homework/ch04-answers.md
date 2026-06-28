# 第四章 课后作业参考答案

---

### 5. 考虑下面文法 $G_1$：
$$
\begin{aligned}
S &\to a \mid \wedge \mid (T) \\
T &\to T, S \mid S
\end{aligned}
$$

**(1) 消去 $G_1$ 的左递归。然后，对每个非终结符，写出不带回溯的递归子程序。**
**(2) 经改写后的文法是否是 $\text{LL}(1)$ 的？给出它的预测分析表。**

**解答**：

#### (1) 消去直接左递归并写出递归下降子程序
文法中非终结符 $T$ 的产生式含有直接左递归：$T \to T, S \mid S$。
应用消除左递归的常规公式 $A \to A\alpha \mid \beta \implies A \to \beta A', A' \to \alpha A' \mid \varepsilon$，我们有：
$$ T \to S T' $$
$$ T' \to , S T' \mid \varepsilon $$

消除左递归后的等价文法为：
$$
\begin{aligned}
S &\to a \mid \wedge \mid (T) \\
T &\to S T' \\
T' &\to , S T' \mid \varepsilon
\end{aligned}
$$

**不带回溯的递归下降子程序（伪代码）**：
```pascal
procedure S;
begin
  if lookahead = 'a' then
    match('a')
  else if lookahead = '^' then
    match('^')
  else if lookahead = '(' then
    begin
      match('(');
      T;
      match(')');
    end
  else
    error("Syntax Error in S");
end;

procedure T;
begin
  S;
  T';
end;

procedure T';
begin
  if lookahead = ',' then
    begin
      match(',');
      S;
      T';
    end
  else if lookahead = ')' then
    { 对应 T' -> ε，空匹配，因为 ) 属于 FOLLOW(T') }
    begin end
  else
    error("Syntax Error in T'");
end;
```

#### (2) $\text{LL}(1)$ 判定及预测分析表
首先计算文法非终结符的 $\text{FIRST}$ 与 $\text{FOLLOW}$ 集合：
*   $\text{FIRST}(S) = \{ a, \wedge, ( \}$
*   $\text{FIRST}(T) = \text{FIRST}(S) = \{ a, \wedge, ( \}$
*   $\text{FIRST}(T') = \{ ,, \varepsilon \}$
*   $\text{FOLLOW}(S) = \{ \$, ,, ) \}$
*   $\text{FOLLOW}(T) = \{ ) \}$
*   $\text{FOLLOW}(T') = \text{FOLLOW}(T) = \{ ) \}$

**$\text{LL}(1)$ 判定**：
对于含有选择分支的产生式 $T' \to , S T' \mid \varepsilon$，其两分支选择的 $\text{FIRST}$ 交集为：
$$ \text{FIRST}(, S T') \cap \text{FOLLOW}(T') = \{ , \} \cap \{ ) \} = \emptyset $$
由于对所有非终结符，候选产生式的 $\text{FIRST}$ 集合均两两互不相交，且包含 $\varepsilon$ 的产生式其 $\text{FIRST}$ 与 $\text{FOLLOW}$ 的交集也为空。因此该文法是 **$\text{LL}(1)$ 文法**。

**预测分析表**：

| 非终结符 | $a$ | $\wedge$ | $($ | $)$ | $,$ | $\$$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **$S$** | $S \to a$ | $S \to \wedge$ | $S \to (T)$ | | | |
| **$T$** | $T \to S T'$ | $T \to S T'$ | $T \to S T'$ | | | |
| **$T'$** | | | | $T' \to \varepsilon$ | $T' \to , S T'$ | |

---

### 6. 对下面的文法 $G$：
$$
\begin{aligned}
E &\to T E' \\
E' &\to +E \mid \varepsilon \\
T &\to F T' \\
T' &\to T \mid \varepsilon \\
F &\to P F' \\
F' &\to *F' \mid \varepsilon \\
P &\to (E) \mid a \mid b \mid \wedge
\end{aligned}
$$

**(1) 构造这个文法的每个非终结符的 $\text{FIRST}$ 和 $\text{FOLLOW}$ 集合。**
**(2) 证明这个文法是 $\text{LL}(1)$ 的。**
**(3) 构造它的预测分析表。**
**(4) 构造它的递归下降分析程序。**

**解答**：

#### (1) 计算 $\text{FIRST}$ 与 $\text{FOLLOW}$ 集合
（详细推导见[课本大题-答案](file:///D:/Study/ComputerScience/Computer_2026_Spring_Term/Compiler_Principles/exercises/homework/%E7%BC%96%E8%AF%91%E5%8E%9F%E7%90%86_%E8%AF%BE%E6%9C%AC%E5%A4%A7%E9%A2%98_%E7%AD%94%E6%A1%88.md#1-first-%E4%B8%8E-follow-%E9%9B%86%E5%90%88)）

| 非终结符 | $\text{FIRST}$ 集合 | $\text{FOLLOW}$ 集合 |
| :--- | :--- | :--- |
| **$E$** | $\{ (, a, b, \wedge \}$ | $\{ \$, ) \}$ |
| **$E'$** | $\{ +, \varepsilon \}$ | $\{ \$, ) \}$ |
| **$T$** | $\{ (, a, b, \wedge \}$ | $\{ +, \$, ) \}$ |
| **$T'$** | $\{ (, a, b, \wedge, \varepsilon \}$ | $\{ +, \$, ) \}$ |
| **$F$** | $\{ (, a, b, \wedge \}$ | $\{ (, a, b, \wedge, +, \$, ) \}$ |
| **$F'$** | $\{ *, \varepsilon \}$ | $\{ (, a, b, \wedge, +, \$, ) \}$ |
| **$P$** | $\{ (, a, b, \wedge \}$ | $\{ *, (, a, b, \wedge, +, \$, ) \}$ |

#### (2) 证明是 $\text{LL}(1)$ 文法
文法中凡是具有多个候选产生式的非终结符，需要验证其 $\text{FIRST}$ 与 $\text{FOLLOW}$ 无交集冲突：
1.  **对于 $E' \to +E \mid \varepsilon$**：
    $\text{FIRST}(+E) \cap \text{FOLLOW}(E') = \{ + \} \cap \{ \$, ) \} = \emptyset$。
2.  **对于 $T' \to T \mid \varepsilon$**：
    $\text{FIRST}(T) \cap \text{FOLLOW}(T') = \{ (, a, b, \wedge \} \cap \{ +, \$, ) \} = \emptyset$。
3.  **对于 $F' \to *F' \mid \varepsilon$**：
    $\text{FIRST}(*F') \cap \text{FOLLOW}(F') = \{ * \} \cap \{ (, a, b, \wedge, +, \$, ) \} = \emptyset$。
4.  **对于 $P \to (E) \mid a \mid b \mid \wedge$**：
    各分支选择的首字符集分别为 $\{(\}$、$\{a\}$、$\{b\}$、$\{\wedge\}$，它们两两不相交。

经检验，文法所有冲突均可完全解决，故该文法**是 $\text{LL}(1)$ 文法**。

#### (3) 构造它的预测分析表
（详细预测分析表见[课本大题-答案](file:///D:/Study/ComputerScience/Computer_2026_Spring_Term/Compiler_Principles/exercises/homework/%E7%BC%96%E8%AF%91%E5%8E%9F%E7%90%86_%E8%AF%BE%E6%9C%AC%E5%A4%A7%E9%A2%98_%E7%AD%94%E6%A1%88.md#2-ll1-%E9%A2%84%E6%B5%8B%E5%88%86%E6%9E%90%E8%A1%A8)）

#### (4) 递归下降分析程序
```pascal
procedure E;
begin
  T; E';
end;

procedure E';
begin
  if lookahead = '+' then
    begin match('+'); E; end
  else if lookahead in [')', '$'] then
    { 空匹配 }
  else error;
end;

procedure T;
begin
  F; T';
end;

procedure T';
begin
  if lookahead in ['(', 'a', 'b', '^'] then
    T
  else if lookahead in ['+', '$', ')'] then
    { 空匹配 }
  else error;
end;

procedure F;
begin
  P; F';
end;

procedure F';
begin
  if lookahead = '*' then
    begin match('*'); F'; end
  else if lookahead in ['(', 'a', 'b', '^', '+', '$', ')'] then
    { 空匹配 }
  else error;
end;

procedure P;
begin
  if lookahead = '(' then
    begin match('('); E; match(')'); end
  else if lookahead = 'a' then match('a')
  else if lookahead = 'b' then match('b')
  else if lookahead = '^' then match('^')
  else error;
end;
```

---

### 7. 对下面文法：
$$
\begin{aligned}
\textit{Expr} &\to -\textit{Expr} \mid (\textit{Expr}) \mid \textit{Var} \ \textit{ExprTail} \\
\textit{ExprTail} &\to -\textit{Expr} \mid \varepsilon \\
\textit{Var} &\to \textit{id} \ \textit{VarTail} \\
\textit{VarTail} &\to (\textit{Expr}) \mid \varepsilon
\end{aligned}
$$

**(1) 构造 $\text{LL}(1)$ 分析表。**
**(2) 给出对句子 $\textit{id}--\textit{id}((\textit{id}))$ 的分析过程。**

**解答**：

#### (1) $\text{FIRST}$ / $\text{FOLLOW}$ 及 $\text{LL}(1)$ 预测分析表
*   **各非终结符的 $\text{FIRST}$ 与 $\text{FOLLOW}$**：
    *   $\text{FIRST}(\textit{Expr}) = \{ -, (, \textit{id} \}$
    *   $\text{FIRST}(\textit{ExprTail}) = \{ -, \varepsilon \}$
    *   $\text{FIRST}(\textit{Var}) = \{ \textit{id} \}$
    *   $\text{FIRST}(\textit{VarTail}) = \{ (, \varepsilon \}$
    *   $\text{FOLLOW}(\textit{Expr}) = \{ \$, ) \}$
    *   $\text{FOLLOW}(\textit{ExprTail}) = \text{FOLLOW}(\textit{Expr}) = \{ \$, ) \}$
    *   $\text{FOLLOW}(\textit{Var}) = (\text{FIRST}(\textit{ExprTail}) \setminus \{\varepsilon\}) \cup \text{FOLLOW}(\textit{Expr}) = \{ -, \$, ) \}$
    *   $\text{FOLLOW}(\textit{VarTail}) = \text{FOLLOW}(\textit{Var}) = \{ -, \$, ) \}$

*   **$\text{LL}(1)$ 预测分析表**：

| 非终结符 | `id` | `-` | `(` | `)` | `$` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **$\textit{Expr}$** | $\textit{Expr} \to \textit{Var} \ \textit{ExprTail}$ | $\textit{Expr} \to -\textit{Expr}$ | $\textit{Expr} \to (\textit{Expr})$ | | |
| **$\textit{ExprTail}$** | | $\textit{ExprTail} \to -\textit{Expr}$ | | $\textit{ExprTail} \to \varepsilon$ | $\textit{ExprTail} \to \varepsilon$ |
| **$\textit{Var}$** | $\textit{Var} \to \textit{id} \ \textit{VarTail}$ | | | | |
| **$\textit{VarTail}$** | | $\textit{VarTail} \to \varepsilon$ | $\textit{VarTail} \to (\textit{Expr})$ | $\textit{VarTail} \to \varepsilon$ | $\textit{VarTail} \to \varepsilon$ |

#### (2) 句子 $\textit{id}--\textit{id}((\textit{id}))$ 的分析步骤过程

下表展示了使用分析栈对句子进行分析的过程（其中 `#` 代表栈底标志）：

| 步骤 | 符号栈 (从右至左压栈) | 剩余输入串 | 所用产生式 / 动作 |
| :--- | :--- | :--- | :--- |
| **1** | `#` $\textit{Expr}$ | `id - - id ( ( id ) ) #` | $\textit{Expr} \to \textit{Var} \ \textit{ExprTail}$ |
| **2** | `#` $\textit{ExprTail}$ $\textit{Var}$ | `id - - id ( ( id ) ) #` | $\textit{Var} \to \textit{id} \ \textit{VarTail}$ |
| **3** | `#` $\textit{ExprTail}$ $\textit{VarTail}$ `id` | `id - - id ( ( id ) ) #` | 匹配终结符 `id` (移进) |
| **4** | `#` $\textit{ExprTail}$ $\textit{VarTail}$ | `- - id ( ( id ) ) #` | $\textit{VarTail} \to \varepsilon$ (因 `-` $\in$ $\text{FOLLOW}(\textit{VarTail})$) |
| **5** | `#` $\textit{ExprTail}$ | `- - id ( ( id ) ) #` | $\textit{ExprTail} \to -\textit{Expr}$ |
| **6** | `#` $\textit{Expr}$ `-` | `- - id ( ( id ) ) #` | 匹配终结符 `-` (移进) |
| **7** | `#` $\textit{Expr}$ | `- id ( ( id ) ) #` | $\textit{Expr} \to -\textit{Expr}$ |
| **8** | `#` $\textit{Expr}$ `-` | `- id ( ( id ) ) #` | 匹配终结符 `-` (移进) |
| **9** | `#` $\textit{Expr}$ | `id ( ( id ) ) #` | $\textit{Expr} \to \textit{Var} \ \textit{ExprTail}$ |
| **10** | `#` $\textit{ExprTail}$ $\textit{Var}$ | `id ( ( id ) ) #` | $\textit{Var} \to \textit{id} \ \textit{VarTail}$ |
| **11** | `#` $\textit{ExprTail}$ $\textit{VarTail}$ `id` | `id ( ( id ) ) #` | 匹配终结符 `id` (移进) |
| **12** | `#` $\textit{ExprTail}$ $\textit{VarTail}$ | `( ( id ) ) #` | $\textit{VarTail} \to (\textit{Expr})$ (因 `(` $\in$ $\text{FIRST}((\textit{Expr}))$) |
| **13** | `#` $\textit{ExprTail}$ `)` $\textit{Expr}$ `(` | `( ( id ) ) #` | 匹配终结符 `(` (移进) |
| **14** | `#` $\textit{ExprTail}$ `)` $\textit{Expr}$ | `( id ) ) #` | $\textit{Expr} \to (\textit{Expr})$ |
| **15** | `#` $\textit{ExprTail}$ `)` `)` $\textit{Expr}$ `(` | `( id ) ) #` | 匹配终结符 `(` (移进) |
| **16** | `#` $\textit{ExprTail}$ `)` `)` $\textit{Expr}$ | `id ) ) #` | $\textit{Expr} \to \textit{Var} \ \textit{ExprTail}$ |
| **17** | `#` $\textit{ExprTail}$ `)` `)` $\textit{ExprTail}$ $\textit{Var}$ | `id ) ) #` | $\textit{Var} \to \textit{id} \ \textit{VarTail}$ |
| **18** | `#` $\textit{ExprTail}$ `)` `)` $\textit{ExprTail}$ $\textit{VarTail}$ `id` | `id ) ) #` | 匹配终结符 `id` (移进) |
| **19** | `#` $\textit{ExprTail}$ `)` `)` $\textit{ExprTail}$ $\textit{VarTail}$ | `) ) #` | $\textit{VarTail} \to \varepsilon$ (因 `)` $\in$ $\text{FOLLOW}(\textit{VarTail})$) |
| **20** | `#` $\textit{ExprTail}$ `)` `)` $\textit{ExprTail}$ | `) ) #` | $\textit{ExprTail} \to \varepsilon$ (因 `)` $\in$ $\text{FOLLOW}(\textit{ExprTail})$) |
| **21** | `#` $\textit{ExprTail}$ `)` `)` | `) ) #` | 匹配终结符 `)` (移进) |
| **22** | `#` $\textit{ExprTail}$ `)` | `) #` | 匹配终结符 `)` (移进) |
| **23** | `#` $\textit{ExprTail}$ | `#` | $\textit{ExprTail} \to \varepsilon$ (因 `#` $\in$ $\text{FOLLOW}(\textit{ExprTail})$) |
| **24** | `#` | `#` | 分析成功结束，句子合法被接受 |

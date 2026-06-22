## q12

**证明：**
从文法开始符号 $E$ 出发，存在如下推导过程：


$$E \Rightarrow E + T \Rightarrow E + T * F$$


因此，$E + T * F$ 是该文法的一个句型。

**短语：**
$T * F$ ， $E + T * F$

**直接短语：**
$T * F$

**句柄：**
$T * F$


----

## q13

### (1) 最左推导和最右推导

**对于串 $(a, (a, a))$：**

**最左推导：**

$$\begin{aligned}
S &\Rightarrow (T) \\
&\Rightarrow (T, S) \\
&\Rightarrow (S, S) \\
&\Rightarrow (a, S) \\
&\Rightarrow (a, (T)) \\
&\Rightarrow (a, (T, S)) \\
&\Rightarrow (a, (S, S)) \\
&\Rightarrow (a, (a, S)) \\
&\Rightarrow (a, (a, a))
\end{aligned}$$

**最右推导：**

$$\begin{aligned}
S &\Rightarrow (T) \\
&\Rightarrow (T, S) \\
&\Rightarrow (T, (T)) \\
&\Rightarrow (T, (T, S)) \\
&\Rightarrow (T, (T, a)) \\
&\Rightarrow (T, (S, a)) \\
&\Rightarrow (T, (a, a)) \\
&\Rightarrow (S, (a, a)) \\
&\Rightarrow (a, (a, a))
\end{aligned}$$

---

**对于串 $(((a, a), \wedge, (a)), a)$：**

**最左推导：**

$$\begin{aligned}
S &\Rightarrow (T) \\
&\Rightarrow (T, S) \\
&\Rightarrow (S, S) \\
&\Rightarrow ((T), S) \\
&\Rightarrow ((T, S), S) \\
&\Rightarrow ((T, S, S), S) \\
&\Rightarrow ((S, S, S), S) \\
&\Rightarrow (((T), S, S), S) \\
&\Rightarrow (((T, S), S, S), S) \\
&\Rightarrow (((S, S), S, S), S) \\
&\Rightarrow (((a, S), S, S), S) \\
&\Rightarrow (((a, a), S, S), S) \\
&\Rightarrow (((a, a), \wedge, S), S) \\
&\Rightarrow (((a, a), \wedge, (T)), S) \\
&\Rightarrow (((a, a), \wedge, (S)), S) \\
&\Rightarrow (((a, a), \wedge, (a)), S) \\
&\Rightarrow (((a, a), \wedge, (a)), a)
\end{aligned}$$

**最右推导：**

$$\begin{aligned}
S &\Rightarrow (T) \\
&\Rightarrow (T, S) \\
&\Rightarrow (T, a) \\
&\Rightarrow (S, a) \\
&\Rightarrow ((T), a) \\
&\Rightarrow ((T, S), a) \\
&\Rightarrow ((T, (T)), a) \\
&\Rightarrow ((T, (S)), a) \\
&\Rightarrow ((T, (a)), a) \\
&\Rightarrow ((T, S, (a)), a) \\
&\Rightarrow ((T, \wedge, (a)), a) \\
&\Rightarrow ((S, \wedge, (a)), a) \\
&\Rightarrow (((T), \wedge, (a)), a) \\
&\Rightarrow (((T, S), \wedge, (a)), a) \\
&\Rightarrow (((T, a), \wedge, (a)), a) \\
&\Rightarrow (((S, a), \wedge, (a)), a) \\
&\Rightarrow (((a, a), \wedge, (a)), a)
\end{aligned}$$

---

### (2) $(((a, a), \wedge, (a)), a)$ 的规范归约及每一步的句柄

规范归约序列（最右推导的逆过程）及每步对应的句柄如下：

| 规范归约（当前句型）         | 句柄     | 归约所用产生式 |
| ---------------------------- | -------- | -------------- |
| $(((a, a), \wedge, (a)), a)$ | $a$      | $S \to a$      |
| $(((S, a), \wedge, (a)), a)$ | $S$      | $T \to S$      |
| $(((T, a), \wedge, (a)), a)$ | $a$      | $S \to a$      |
| $(((T, S), \wedge, (a)), a)$ | $T, S$   | $T \to T, S$   |
| $(((T), \wedge, (a)), a)$    | $(T)$    | $S \to (T)$    |
| $((S, \wedge, (a)), a)$      | $S$      | $T \to S$      |
| $((T, \wedge, (a)), a)$      | $\wedge$ | $S \to \wedge$ |
| $((T, S, (a)), a)$           | $T, S$   | $T \to T, S$   |
| $((T, (a)), a)$              | $a$      | $S \to a$      |
| $((T, (S)), a)$              | $S$      | $T \to S$      |
| $((T, (T)), a)$              | $(T)$    | $S \to (T)$    |
| $((T, S), a)$                | $T, S$   | $T \to T, S$   |
| $((T), a)$                   | $(T)$    | $S \to (T)$    |
| $(S, a)$                     | $S$      | $T \to S$      |
| $(T, a)$                     | $a$      | $S \to a$      |
| $(T, S)$                     | $T, S$   | $T \to T, S$   |
| $(T)$                        | $(T)$    | $S \to (T)$    |
| $S$                          | -        | -              |

---

### "移进—归约"的过程

| 步骤 | 符号栈         | 剩余输入串                    | 动作                |
| ---- | -------------- | ----------------------------- | ------------------- |
| 1    | `#`            | `(((a, a), \wedge, (a)), a)#` | 移进                |
| 2    | `#(`           | `((a, a), \wedge, (a)), a)#`  | 移进                |
| 3    | `#((`          | `(a, a), \wedge, (a)), a)#`   | 移进                |
| 4    | `#(((`         | `a, a), \wedge, (a)), a)#`    | 移进                |
| 5    | `#(((a`        | `, a), \wedge, (a)), a)#`     | 归约 $S \to a$      |
| 6    | `#(((S`        | `, a), \wedge, (a)), a)#`     | 归约 $T \to S$      |
| 7    | `#(((T`        | `, a), \wedge, (a)), a)#`     | 移进                |
| 8    | `#(((T,`       | `a), \wedge, (a)), a)#`       | 移进                |
| 9    | `#(((T, a`     | `), \wedge, (a)), a)#`        | 归约 $S \to a$      |
| 10   | `#(((T, S`     | `), \wedge, (a)), a)#`        | 归约 $T \to T, S$   |
| 11   | `#(((T`        | `), \wedge, (a)), a)#`        | 移进                |
| 12   | `#(((T)`       | `, \wedge, (a)), a)#`         | 归约 $S \to (T)$    |
| 13   | `#((S`         | `, \wedge, (a)), a)#`         | 归约 $T \to S$      |
| 14   | `#((T`         | `, \wedge, (a)), a)#`         | 移进                |
| 15   | `#((T,`        | `\wedge, (a)), a)#`           | 移进                |
| 16   | `#((T, \wedge` | `, (a)), a)#`                 | 归约 $S \to \wedge$ |
| 17   | `#((T, S`      | `, (a)), a)#`                 | 归约 $T \to T, S$   |
| 18   | `#((T`         | `, (a)), a)#`                 | 移进                |
| 19   | `#((T,`        | `(a)), a)#`                   | 移进                |
| 20   | `#((T, (`      | `a)), a)#`                    | 移进                |
| 21   | `#((T, (a`     | `)), a)#`                     | 归约 $S \to a$      |
| 22   | `#((T, (S`     | `)), a)#`                     | 归约 $T \to S$      |
| 23   | `#((T, (T`     | `)), a)#`                     | 移进                |
| 24   | `#((T, (T)`    | `, a)#`                       | 归约 $S \to (T)$    |
| 25   | `#((T, S`      | `, a)#`                       | 归约 $T \to T, S$   |
| 26   | `#((T`         | `, a)#`                       | 移进                |
| 27   | `#((T)`        | `, a)#`                       | 归约 $S \to (T)$    |
| 28   | `#(S`          | `, a)#`                       | 归约 $T \to S$      |
| 29   | `#(T`          | `, a)#`                       | 移进                |
| 30   | `#(T,`         | `a)#`                         | 移进                |
| 31   | `#(T, a`       | `)#`                          | 归约 $S \to a$      |
| 32   | `#(T, S`       | `)#`                          | 归约 $T \to T, S$   |
| 33   | `#(T`          | `)#`                          | 移进                |
| 34   | `#(T)`         | `#`                           | 归约 $S \to (T)$    |
| 35   | `#S`           | `#`                           | 接受                |

---

### 语法树自下而上的构造过程

随着规范归约的进行，语法树自下而上逐步生成子树，构造顺序如下：

1. 为第1个 $a$ 构造子树：$S \to a$
2. 构造子树：$T \to S$
3. 为第2个 $a$ 构造子树：$S \to a$
4. 将步骤2的 $T$ 与步骤3的 $S$ 结合，构造子树：$T \to T, S$
5. 为外层括号结合步骤4的 $T$，构造子树：$S \to (T)$
6. 构造子树：$T \to S$
7. 为 $\wedge$ 构造子树：$S \to \wedge$
8. 将步骤6的 $T$ 与步骤7的 $S$ 结合，构造子树：$T \to T, S$
9. 为第3个 $a$ 构造子树：$S \to a$
10. 构造子树：$T \to S$
11. 为外层括号结合步骤10的 $T$，构造子树：$S \to (T)$
12. 将步骤8的 $T$ 与步骤11的 $S$ 结合，构造子树：$T \to T, S$
13. 为外层括号结合步骤12的 $T$，构造子树：$S \to (T)$
14. 构造子树：$T \to S$
15. 为第4个（最后一个）$a$ 构造子树：$S \to a$
16. 将步骤14的 $T$ 与步骤15的 $S$ 结合，构造子树：$T \to T, S$
17. 为最外层括号结合步骤16的 $T$，构造最终的树根：$S \to (T)$

----

## q15

### (1) LR(0) 项目

增加拓广文法产生式 $S' \to S$。该文法的所有 LR(0) 项目共 12 个：

1. $S' \to \cdot S$
2. $S' \to S \cdot$
3. $S \to \cdot AS$
4. $S \to A \cdot S$
5. $S \to AS \cdot$
6. $S \to \cdot b$
7. $S \to b \cdot$
8. $A \to \cdot SA$
9. $A \to S \cdot A$
10. $A \to SA \cdot$
11. $A \to \cdot a$
12. $A \to a \cdot$

---

### (2) LR(0) 项目集规范族及识别活前缀的 DFA

**LR(0) 项目集规范族：**

* $I_0$:
$S' \to \cdot S$
$S \to \cdot AS$
$S \to \cdot b$
$A \to \cdot SA$
$A \to \cdot a$
* $I_1$:
$S' \to S \cdot$
$A \to S \cdot A$
$S \to \cdot AS$
$S \to \cdot b$
$A \to \cdot SA$
$A \to \cdot a$
* $I_2$:
$S \to A \cdot S$
$S \to \cdot AS$
$S \to \cdot b$
$A \to \cdot SA$
$A \to \cdot a$
* $I_3$:
$A \to a \cdot$
* $I_4$:
$S \to b \cdot$
* $I_5$:
$A \to SA \cdot$
$S \to A \cdot S$
$S \to \cdot AS$
$S \to \cdot b$
$A \to \cdot SA$
$A \to \cdot a$
* $I_6$:
$A \to S \cdot A$
$S \to \cdot AS$
$S \to \cdot b$
$A \to \cdot SA$
$A \to \cdot a$
* $I_7$:
$S \to AS \cdot$
$A \to S \cdot A$
$S \to \cdot AS$
$S \to \cdot b$
$A \to \cdot SA$
$A \to \cdot a$

**识别活前缀的 DFA 状态转移方程：**

| 状态      | 接收 $S$ | 接收 $A$ | 接收 $a$ | 接收 $b$ |
| --------- | -------- | -------- | -------- | -------- |
| **$I_0$** | $I_1$    | $I_2$    | $I_3$    | $I_4$    |
| **$I_1$** | $I_6$    | $I_5$    | $I_3$    | $I_4$    |
| **$I_2$** | $I_7$    | $I_2$    | $I_3$    | $I_4$    |
| **$I_3$** | -        | -        | -        | -        |
| **$I_4$** | -        | -        | -        | -        |
| **$I_5$** | $I_7$    | $I_2$    | $I_3$    | $I_4$    |
| **$I_6$** | $I_6$    | $I_5$    | $I_3$    | $I_4$    |
| **$I_7$** | $I_6$    | $I_5$    | $I_3$    | $I_4$    |

---

### (3) 这个文法是 SLR 的吗？若是，构造出它的 SLR 分析表。

**答：不是 SLR 文法。**

**证明过程：**
首先求非终结符的 FOLLOW 集：

* $\text{FOLLOW}(S) = \{\$, a, b\}$
* $\text{FOLLOW}(A) = \{a, b\}$

观察项目集 $I_5$：
$I_5$ 中包含归约项目 $A \to SA \cdot$ ，同时存在针对终结符 $a, b$ 的移进操作（$\text{GO}(I_5, a) = I_3, \text{GO}(I_5, b) = I_4$）。
因为 $a, b \in \text{FOLLOW}(A)$，所以在 SLR 构造规则下，当面临输入符号 $a$ 或 $b$ 时，既需要移进，又需要按 $A \to SA$ 进行归约。
存在无法解决的**移进-归约冲突**，故不是 SLR 文法，不需要构造分析表。

---

### (4) 这个文法是 LALR 或 LR(1) 的吗？

**答：不是 LALR，也不是 LR(1) 文法。**

**原因：**
该文法是一个**二义性文法**。对于同一个句子（例如句子 $abab$），可以构造出两棵及以上的不同语法树（存在不同的最左推导）。二义性文法必定存在无论如何也无法消除的冲突，因此它绝对不可能是 LR(1) 文法，自然也不可能是 LALR 文法。


## q17

**证明：**

**1. 构造拓广文法及 LR(0) 项目集规范族**

增加拓广产生式 $S' \to S$。

* $I_0$:
$S' \to \cdot S$
$S \to \cdot A$
$A \to \cdot Ab$
$A \to \cdot bBa$
* $I_1$:
$S' \to S \cdot$
* $I_2$:
$S \to A \cdot$
$A \to A \cdot b$
* $I_3$:
$A \to b \cdot Ba$
$B \to \cdot aAc$
$B \to \cdot a$
$B \to \cdot aAb$
* $I_4$:
$A \to Ab \cdot$
* $I_5$:
$A \to bB \cdot a$
* $I_6$:
$B \to a \cdot Ac$
$B \to a \cdot$
$B \to a \cdot Ab$
$A \to \cdot Ab$
$A \to \cdot bBa$
* $I_7$:
$A \to bBa \cdot$
* $I_8$:
$B \to aA \cdot c$
$B \to aA \cdot b$
$A \to A \cdot b$
* $I_9$:
$B \to aAc \cdot$
* $I_{10}$:
$B \to aAb \cdot$
$A \to Ab \cdot$

状态转移补充说明（仅列出产生新状态的转移）：
$\text{GO}(I_0, S) = I_1$
$\text{GO}(I_0, A) = I_2$
$\text{GO}(I_0, b) = I_3$
$\text{GO}(I_2, b) = I_4$
$\text{GO}(I_3, B) = I_5$
$\text{GO}(I_3, a) = I_6$
$\text{GO}(I_5, a) = I_7$
$\text{GO}(I_6, A) = I_8$
$\text{GO}(I_6, b) = I_3$
$\text{GO}(I_8, c) = I_9$
$\text{GO}(I_8, b) = I_{10}$

**2. 证明该文法不是 LR(0) 文法**

观察上述项目集，存在以下冲突：

* 在状态 $I_2$ 中，存在“移进-归约”冲突：面临输入符号 $b$ 时，既可以按 $S \to A$ 归约，又可以移进。
* 在状态 $I_6$ 中，存在“移进-归约”冲突：面临输入符号 $b$ 时，既可以按 $B \to a$ 归约，又可以移进。
* 在状态 $I_{10}$ 中，存在“归约-归约”冲突：既可以按 $B \to aAb$ 归约，也可以按 $A \to Ab$ 归约。

因为存在无法解决的冲突，所以该文法**不是 LR(0) 文法**。

**3. 计算 FOLLOW 集**

$\text{FOLLOW}(S) = \{ \$ \}$
$\text{FOLLOW}(A) = \{ \$, b, c \}$
$\text{FOLLOW}(B) = \{ a \}$

**4. 证明该文法是 SLR(1) 文法**

利用 SLR(1) 分析法尝试消除上述冲突：

* **对于状态 $I_2$：**
归约项目 $S \to A \cdot$ 的后续符号集 $\text{FOLLOW}(S) = \{ \$ \}$。
移进符号为 $b$。
因为 $\{ \$ \} \cap \{ b \} = \emptyset$，所以冲突可解决：面临 $\$$ 时归约，面临 $b$ 时移进。
* **对于状态 $I_6$：**
归约项目 $B \to a \cdot$ 的后续符号集 $\text{FOLLOW}(B) = \{ a \}$。
移进符号为 $b$。
因为 $\{ a \} \cap \{ b \} = \emptyset$，所以冲突可解决：面临 $a$ 时归约，面临 $b$ 时移进。
* **对于状态 $I_{10}$：**
归约项目 $B \to aAb \cdot$ 的后续符号集 $\text{FOLLOW}(B) = \{ a \}$。
归约项目 $A \to Ab \cdot$ 的后续符号集 $\text{FOLLOW}(A) = \{ \$, b, c \}$。
因为 $\{ a \} \cap \{ \$, b, c \} = \emptyset$，所以冲突可解决：面临 $a$ 时按 $B \to aAb$ 归约；面临 $\$ , b, c$ 时按 $A \to Ab$ 归约。

因为该文法的所有冲突均能通过 SLR(1) 方法（检查 FOLLOW 集）得到完全解决，所以该文法**是 SLR(1) 文法**。得证。
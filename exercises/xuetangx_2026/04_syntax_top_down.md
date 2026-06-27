# 学堂在线测试 —— 编译原理

## 语法分析----自上而下分析 习题

---

## 一、 单项选择题（本题共 15 小题，每小题 1 分，共 15 分）

**1. 编译过程中，语法分析器的任务是 ( )。**
① 分析单词是怎样构成的
② 分析单词串是如何构成语句和说明的
③ 分析语句和说明是如何构成程序的
④ 分析程序的结构

* A. ②③
* B. ②③④
* C. ①②③
* D. ①②③④

**2. 在高级语言编译程序常用的语法分析方法中，预测分析方法属于 ( )。**

* A. 自左至右分析法
* B. 自上而下分析法
* C. 自下而上分析法
* D. 自右至左分析法

**3. 关于 LL(1) 文法，以下说法正确的是 ( )。**

* A. 使用 LL(1) 文法能够进行有效的自上而下语法分析
* B. 使用 LL(1) 文法能够进行有效的自下而上语法分析
* C. LL(1) 文法可以含有左递归
* D. 任何上下文无关文法都一定是 LL(1) 的

**4. 下列哪项不属于语法分析的方法 ( )。**

* A. 递归下降分析法
* B. LR 分析法
* C. 乔姆斯基范式分析法
* D. 算符优先分析法

**5. 自顶向下语法分析中，避免回溯的关键是 ( )。**

* A. 采用 LL(1) 文法
* B. 消除左递归
* C. 提取左因子
* D. 以上都是

**6. 下列哪种方法不属于自顶向下的语法分析方法 ( )。**

* A. 递归下降分析法
* B. LL(1) 分析法
* C. SLR(1) 分析法
* D. 预测分析法

**7. LL(1) 文法中的 “1” 表示 ( )。**

* A. 分析过程中每次回溯 1 次
* B. 文法是 1 型文法（上下文有关文法）
* C. 分析时每次向前看 1 个输入符号
* D. 产生式的右部长度不超过 1

**8. 下列关于左递归文法的说法，正确的是 ( )。**

* A. 左递归文法可以直接用于 LL(1) 分析
* B. 左递归是指产生式左部符号在右部开头出现（如 $A \to A\alpha$）
* C. 所有左递归文法都无法进行语法分析
* D. 左递归只会出现在上下文无关文法中

**9. 下列哪种文法可能存在二义性 ( )。**

* A. 一个句子对应两棵不同的语法树
* B. 文法中存在左递归
* C. 文法中存在 $\varepsilon$ 产生式
* D. 文法是 LL(1) 文法

**10. 在 LL(1) 分析中，若对于非终结符 $A$ 和输入符号 $a$，有多个产生式 $A \to \alpha$ 都满足 $\text{FIRST}(\alpha)$ 包含 $a$，则该文法 ( )。**

* A. 是 LL(1) 文法
* B. 存在左递归
* C. 存在回溯风险，不符合 LL(1) 条件
* D. 可以直接用于递归下降分析

**11. 编译程序的各个阶段中，______ 阶段的输出是语法树。**

* A. 词法分析
* B. 语法分析
* C. 语义分析
* D. 中间代码生成

**12. 给定产生式 $A \to \alpha B \beta$，计算 $\text{FIRST}(\alpha \beta)$ 时，以下哪项是正确的？**

* A. 如果 $\alpha$ 不能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha \beta) = \text{FIRST}(\alpha)$
* B. 如果 $\alpha$ 能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha \beta) = (\text{FIRST}(\alpha) \setminus \{\varepsilon\}) \cup \text{FIRST}(\beta)$
* C. 无论 $\alpha$ 能否推导出 $\varepsilon$，$\text{FIRST}(\alpha \beta)$ 都等于 $\text{FIRST}(\alpha)$
* D. 如果 $\alpha$ 能推导出 $\varepsilon$，则 $\text{FIRST}(\alpha \beta) = \text{FIRST}(\beta)$

**13. 已知文法 $G$：**

$$
\begin{aligned}
S &\to Aa \mid b \\
A &\to Sc \mid d
\end{aligned}
$$

**该文法属于 ( )。**

* A. 直接左递归
* B. 间接左递归
* C. 无左递归
* D. 既是直接左递归也是间接左递归

**14. 若文法 $G$ 经消除左递归后得到文法 $G'$，则下列说法正确的是 ( )。**

* A. $G$ 和 $G'$ 的终结符集不同
* B. $G$ 和 $G'$ 产生的语言完全相同
* C. $G$ 和 $G'$ 的非终结符集相同
* D. $G'$ 一定是 LL(1) 文法

**15. 递归下降分析法无法处理含左递归的文法，其根本原因是 ( )。**

* A. 左递归会导致文法二义性
* B. 左递归会使递归调用陷入无限循环
* C. 左递归会增加语法分析的时间复杂度
* D. 左递归会减少产生式的数量

---

## 二、 多项选择题（本题共 2 小题，每小题 2 分，共 4 分。多选、少选、错选均不得分）

**1. 计算非终结符 $A$ 的 $\text{FOLLOW}$ 集时，考虑产生式 $B \to \alpha A \beta$，以下哪项需要加入 $\text{FOLLOW}(A)$？**

* A. $\text{FIRST}(\beta)$
* B. 如果 $\beta$ 能推导出 $\varepsilon$，则还要加入 $\text{FOLLOW}(B)$
* C. $\text{FIRST}(\beta)$ 和 $\text{FOLLOW}(B)$
* D. 如果 $\beta$ 不能推导出 $\varepsilon$，则加入 $\text{FIRST}(\beta)$；如果 $\beta$ 能推导出 $\varepsilon$，则加入 $(\text{FIRST}(\beta) \setminus \{\varepsilon\}) \cup \text{FOLLOW}(B)$

**2. 已知文法 $G[A]$：**

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

---

## 三、 判断题（本题共 3 小题，每小题 1 分，共 3 分）

**1. 每个文法都能改写为 LL(1) 文法。** (   )

**2. 一个 LL(1) 文法一定是无二义的。** (   )

**3. 欲构造行之有效的自上而下分析器，则只需消除左递归。** (   )

---

## 四、 填空题（本题共 2 小题，每小题 2 分，共 4 分）

**1. 语法分析最常用的两类方法是 ______ 和 ______ 分析法。**

**2. 语法分析器的输入是 ______，其输出是 ______。**

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

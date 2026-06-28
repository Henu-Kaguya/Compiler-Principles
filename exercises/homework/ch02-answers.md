# 第二章 课后作业参考答案

---

### 2. 令文法 $G(N)$ 为：

$$
\begin{aligned}
N &\to D \mid ND \\
D &\to 0 \mid 1 \mid 2 \mid 3 \mid 4 \mid 5 \mid 6 \mid 7 \mid 8 \mid 9
\end{aligned}
$$

**(1) $G(N)$ 的语言 $L(G(N))$ 是什么？**
**(2) 给出句子 `0731` 和 `863` 的最左推导和最右推导。**

**解答**：
**(1) $L(G(N))$ 的语言含义**：
$L(G(N))$ 是由非空数字符号串组成的集合，即允许包含前导零的无符号整数集合。

**(2) 最左推导与最右推导**：

* **对于句子 `0731`**：
  * **最左推导**：
    $$
    \begin{aligned}
    N &\Rightarrow ND \\
    &\Rightarrow NDD \\
    &\Rightarrow NDDD \\
    &\Rightarrow DDDD \\
    &\Rightarrow 0DDD \\
    &\Rightarrow 07DD \\
    &\Rightarrow 073D \\
    &\Rightarrow 0731
    \end{aligned}
    $$
  * **最右推导**：
    $$
    \begin{aligned}
    N &\Rightarrow ND \\
    &\Rightarrow N1 \\
    &\Rightarrow ND1 \\
    &\Rightarrow N31 \\
    &\Rightarrow ND31 \\
    &\Rightarrow N731 \\
    &\Rightarrow D731 \\
    &\Rightarrow 0731
    \end{aligned}
    $$
* **对于句子 `863`**：
  * **最左推导**：
    $$
    \begin{aligned}
    N &\Rightarrow ND \\
    &\Rightarrow NDD \\
    &\Rightarrow DDD \\
    &\Rightarrow 8DD \\
    &\Rightarrow 86D \\
    &\Rightarrow 863
    \end{aligned}
    $$
  * **最右推导**：
    $$
    \begin{aligned}
    N &\Rightarrow ND \\
    &\Rightarrow N3 \\
    &\Rightarrow ND3 \\
    &\Rightarrow N63 \\
    &\Rightarrow D63 \\
    &\Rightarrow 863
    \end{aligned}
    $$

---

### 4. 写一个文法，使其语言是偶数集，且每个偶数不以 $0$ 开头。

**解答**：
偶数包含一位偶数（如 $0, 2, 4, 6, 8$）与多位偶数。题目规定每个偶数不能以 $0$ 开头，因此除了单零 $0$ 之外，其他偶数均不能有前导零。其末位必须是 $0, 2, 4, 6, 8$ 中的一个。

构造文法 $G[S]$ 如下：

$$
\begin{aligned}
S &\to 0 \mid D_{\text{head}} M D_{\text{even}} \mid D_{\text{even\_nonzero}} \\
M &\to D M \mid \varepsilon \\
D_{\text{even}} &\to 0 \mid 2 \mid 4 \mid 6 \mid 8 \\
D_{\text{even\_nonzero}} &\to 2 \mid 4 \mid 6 \mid 8 \\
D_{\text{head}} &\to 1 \mid 2 \mid 3 \mid 4 \mid 5 \mid 6 \mid 7 \mid 8 \mid 9 \\
D &\to 0 \mid D_{\text{head}}
\end{aligned}
$$

*设计说明：*

* $S \to 0$ 产生单一的偶数 $0$。
* $S \to D_{\text{even\_nonzero}}$ 产生一位非零偶数 $2, 4, 6, 8$。
* $S \to D_{\text{head}} M D_{\text{even}}$ 产生两位以上的偶数，首位限制为非零数字 $D_{\text{head}}$，末位限制为偶数 $D_{\text{even}}$，中间 $M$ 可以为包含 $0$ 在内的任意数字串。

---

### 5. 给出下面语言的相应文法。

1. $L_1 = \{a^n b^n c^i \mid n \ge 1, i \ge 0\}$
2. $L_2 = \{a^i b^n c^n \mid n \ge 1, i \ge 0\}$
3. $L_3 = \{a^n b^n a^m b^m \mid n, m \ge 0\}$
4. $L_4 = \{1^n 0^m 1^m 0^n \mid n, m \ge 0\}$

**解答**：

#### (1) $L_1 = \{a^n b^n c^i \mid n \ge 1, i \ge 0\}$

由前后两个独立部分串接而成，前部为 $\{a^n b^n \mid n \ge 1\}$，后部为 $\{c^i \mid i \ge 0\}$。
文法为：

$$
\begin{aligned}
S &\to X Y \\
X &\to aXb \mid ab \\
Y &\to cY \mid \varepsilon
\end{aligned}
$$

#### (2) $L_2 = \{a^i b^n c^n \mid n \ge 1, i \ge 0\}$

由前部 $\{a^i \mid i \ge 0\}$ 和后部 $\{b^n c^n \mid n \ge 1\}$ 串接而成。
文法为：

$$
\begin{aligned}
S &\to X Y \\
X &\to aX \mid \varepsilon \\
Y &\to bYc \mid bc
\end{aligned}
$$

#### (3) $L_3 = \{a^n b^n a^m b^m \mid n, m \ge 0\}$

可看作是两个形如 $\{a^k b^k \mid k \ge 0\}$ 的结构直接连接。
文法为：

$$
\begin{aligned}
S &\to X X \\
X &\to aXb \mid \varepsilon
\end{aligned}
$$

#### (4) $L_4 = \{1^n 0^m 1^m 0^n \mid n, m \ge 0\}$

采用从外向内嵌套剥离的规则定义。
文法为：

$$
\begin{aligned}
S &\to 1S0 \mid X \\
X &\to 0X1 \mid \varepsilon
\end{aligned}
$$

---

### 7. 令文法 $G(E)$ 为：

$$
\begin{aligned}
E &\to T \mid E + T \mid E - T \\
T &\to F \mid T * F \mid T / F \\
F &\to (E) \mid i
\end{aligned}
$$

**(1) 给出 $i+i*i$、$i*(i+i)$ 的最左推导和最右推导。**
**(2) 给出 $i+i+i$、$i+i*i$ 和 $i-i-i$ 的语法树。**

**解答**：

#### (1) 最左与最右推导

* **对于句子 $i+i*i$**：
  * **最左推导**：
    $$
    \begin{aligned}
    E &\Rightarrow E + T \\
    &\Rightarrow T + T \\
    &\Rightarrow F + T \\
    &\Rightarrow i + T \\
    &\Rightarrow i + T * F \\
    &\Rightarrow i + F * F \\
    &\Rightarrow i + i * F \\
    &\Rightarrow i + i * i
    \end{aligned}
    $$
  * **最右推导**：
    $$
    \begin{aligned}
    E &\Rightarrow E + T \\
    &\Rightarrow E + T * F \\
    &\Rightarrow E + T * i \\
    &\Rightarrow E + F * i \\
    &\Rightarrow E + i * i \\
    &\Rightarrow T + i * i \\
    &\Rightarrow F + i * i \\
    &\Rightarrow i + i * i
    \end{aligned}
    $$
* **对于句子 $i*(i+i)$**：
  * **最左推导**：
    $$
    \begin{aligned}
    E &\Rightarrow T \\
    &\Rightarrow T * F \\
    &\Rightarrow F * F \\
    &\Rightarrow i * F \\
    &\Rightarrow i * (E) \\
    &\Rightarrow i * (E + T) \\
    &\Rightarrow i * (T + T) \\
    &\Rightarrow i * (F + T) \\
    &\Rightarrow i * (i + T) \\
    &\Rightarrow i * (i + F) \\
    &\Rightarrow i * (i + i)
    \end{aligned}
    $$
  * **最右推导**：
    $$
    \begin{aligned}
    E &\Rightarrow T \\
    &\Rightarrow T * F \\
    &\Rightarrow T * (E) \\
    &\Rightarrow T * (E + T) \\
    &\Rightarrow T * (E + F) \\
    &\Rightarrow T * (E + i) \\
    &\Rightarrow T * (T + i) \\
    &\Rightarrow T * (F + i) \\
    &\Rightarrow T * (i + i) \\
    &\Rightarrow F * (i + i) \\
    &\Rightarrow i * (i + i)
    \end{aligned}
    $$

#### (2) 语法树

* **$i+i+i$ 的语法树**：

```
          E
         /|\
        E + T
       /|\   \
      E + T   F
      |   |   |
      T   F   i
      |   |
      F   i
      |
      i
```

* **$i+i*i$ 的语法树**：

```
          E
         /|\
        E + T
        |  /|\
        T T * F
        | |   |
        F F   i
        | |
        i i
```

* **$i-i-i$ 的语法树**：

```
          E
         /|\
        E - T
       /|\   \
      E - T   F
      |   |   |
      T   F   i
      |   |
      F   i
      |
      i
```

---

### 10. 证明下面的文法是二义的：

$$
S \to iSeS \mid iS \mid i
$$

**证明**：
要证明一个文法是二义的，只需证明该文法存在某个句子对应两棵不同的语法分析树（或存在两个不同的最左推导）。

对于句子 $i \ i \ e \ i$（或者 $i \ i \ i \ e \ i$），我们证明它存在两棵不同的语法树：

* **最左推导 1**（先选择产生式 $S \to iSeS$）：
  $$
  \begin{aligned}
  S &\Rightarrow iSeS \\
  &\Rightarrow i(iS)eS \\
  &\Rightarrow i(ii)eS \\
  &\Rightarrow i(ii)e(i) \\
  &= i \ i \ i \ e \ i
  \end{aligned}
  $$

  对应的语法树结构：

```
          S
       / / \ \
      i S   e S
       / \    |
      i   S   i
          |
          i
```

* **最左推导 2**（先选择产生式 $S \to iS$）：
  $$
  \begin{aligned}
  S &\Rightarrow iS \\
  &\Rightarrow i(iSeS) \\
  &\Rightarrow ii(i)eS \\
  &\Rightarrow ii(i)e(i) \\
  &= i \ i \ i \ e \ i
  \end{aligned}
  $$

  对应的语法树结构：

```
          S
         / \
        i   S
         / / \ \
        i S   e S
          |     |
          i     i
```

由于对于句子 $i \ i \ i \ e \ i$ 该文法能构造出两棵不同结构的语法分析树（这对应着经典的“悬空 else”问题，即 $e$ 归属于内层还是外层 $i$），因此该文法是**二义文法**。

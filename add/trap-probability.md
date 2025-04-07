# Distribuição de Probabilidades da função armadilha de ordem $k$

Nesta nota, deduzimos a probabilidade de $f_k(x)=r$ sendo $f_k:\mathbb{Z}_2^n\rightarrow\mathbb{Z}$ definida por:

$$
f_k(x) := \sum_{i=1}^{n/k} \text{trap}_k\left( \sum_{j=1}^k x_{(i-1)k + j} \right)
$$

onde,


$$
\text{trap}_k(u) =
\begin{cases}
k, & \text{se } u = k, \\
k - 1 - u, & \text{se } 0 \le u < k.
\end{cases}
$$

Isto é, queremos deduzir a probabilidade:

$$
P(f_k(x) = r), \quad \text{com } x \in \mathbb{Z}_2^n,\ r \in \lbrace0,1,\dots,mk\rbrace, \text{ onde } m = n/k.
$$

---

## Definições e estrutura

### 1. Variável de entrada
$$
x = (x_1, x_2, \ldots, x_n) \in \mathbb{Z}_2^n
$$

É um vetor aleatório uniformemente distribuído — todas as $2^n$ combinações têm mesma probabilidade.


### 2. Distribuição da Função OneMax

Seja $\Omega:\mathbb{Z}_2^n\rightarrow\mathbb{Z}$ definida por:

$$
\Omega(x):=\sum_{i=1}^n x_i
$$

A probabilidade $\Omega(x)=r$ com $r \in \lbrace0,1,\dots,n\rbrace$ é dada por:

1. O número de vetores que satisfazem $\Omega(x)=r$ é $\binom{n}{r}$. Pois esta é a contagem de combinações do vetor $x$ com exatamente $r$ componentes iguais a $1$.

2. Cada vetor tem probabilidade $\frac{1}{2^n}$. Supondo seleção aleatória do $x$, isto é, $x \sim\mathcal{U}(0,n)$.

Logo,

$$
P\big(\Omega(x)=r\big)=\binom{n}{r}\frac{1}{2^n}=\frac{n!}{2^n r!(n-r)!}.
$$

### 3. Divisão em blocos


Definimos $m$ o número de blocos de tamnho $k$:

$$
m := \frac{n}{k}.
$$

Para cada bloco $i = 1, \dots, m$, temos:

$$
s_i := \sum_{j=1}^{k} x_{(i-1)k + j},\quad \text{o número de uns no bloco $i$}
$$

Assim cada $s_i \in \lbrace0,1,\dots,k\rbrace$, é resultado de uma OneMax e segue distribuição binomial $\mathcal{B}(k, 1/2)$.

---


## Objetivo

Calcular:

$$
P\left( \sum_{i=1}^m \text{trap}_k(s_i) = r \right)
$$

com $s_i \sim \mathcal{B}(k, 1/2)$, independentes.


### 1 – Distribuição de $\text{trap}_k(s_i)$

Seja $T_i := \text{trap}_k(s_i)$

Vamos calcular a distribuição de $T_i$.

Como $s_i \sim B(k, 1/2)$, temos:

$$
P(s_i = u) = \binom{k}{u} \cdot \frac{1}{2^k}, \quad u = 0, 1, \dots, k
$$

E usando a definição da trap:

- Se $u = k$, então $\text{trap}_k(u) = k$, com probabilidade $P(s_i = k)$
- Se $u < k$, então $\text{trap}_k(u) = k - 1 - u$, com probabilidade $P(s_i = u)$

Logo, podemos definir a distribuição discreta de $T_i$:

$$
P(T_i = r) = 
\begin{cases}
\frac{1}{2^k}\binom{k}{k} = \frac{1}{2^k}, & \text{se } r = k, \\
\frac{\binom{k}{u}}{2^k}, & \text{se } r = k - 1 - u,\ u < k.
\end{cases}
$$

Todo $r \in \lbrace0, 1, \dots, k-1\rbrace$ é mapeado por $u = k - 1 - r$, então:

$$
P(T_i = r) =
\begin{cases}
\frac{1}{2^k}, & \text{se } r = k, \\
\frac{\binom{k}{k - 1 - r}}{2^k}, & \text{se } 0 \le r < k.
\end{cases}
$$



## 2 – Soma de $m$ variáveis independentes $T_1 + T_2 + \cdots + T_m$

Como os $T_i$ são independentes e idênticos (i.i.d.), a soma:

$$
f_k(x) = \sum_{i=1}^m T_i
$$

é a soma de $m$ variáveis i.i.d. discretas.

Logo, a distribuição de $f_k(x)$ é a **convolução** $m$-vezes da distribuição de $T_1$:

$$
P(f_k(x) = r) = \left(P_{T_1} * P_{T_2} * \cdots * P_{T_m}\right)(r) = P_{T}^{(*m)}(r)
$$

---

## Resultado final

Seja $P_{\text{trap}_k}$ o vetor de distribuição discreta de $\text{trap}_k(s_i)$. Então:

$$
P(f_k(x) = r) = P_{\text{trap}_k}^{(*m)}(r)
$$

Esse método nos permite calcular a distribuição $P(f_k(x)=r)$ para qualquer $n$ e $k$ com $k \mid n$, sem gerar todos os $2^n$ vetores.

---

## Revisão sobre Convolução

Excelente! A **convolução** é um conceito fundamental em probabilidade, especialmente quando estamos lidando com **somas de variáveis aleatórias independentes**. Vamos construir a ideia passo a passo, com foco na intuição e rigor matemático 👇


### 1. Contexto geral

Suponha que temos duas variáveis aleatórias discretas **independentes**:

- $X$ com distribuição $P_X(x)$
- $Y$ com distribuição $P_Y(y)$

Queremos saber a distribuição da soma $Z = X + Y$.


### 2. Definição da convolução

A **distribuição de $Z = X + Y$** é dada pela **convolução** de $P_X$ e $P_Y$:

$$
P_Z(z) = (P_X * P_Y)(z) = \sum_{x} P_X(x) \cdot P_Y(z - x)
$$

Em outras palavras:

- Para cada valor $z$, somamos todos os pares $(x, y)$ tais que $x + y = z$.
- Como $X$ e $Y$ são independentes, a probabilidade conjunta é o produto das marginais: $P(X = x, Y = z - x) = P_X(x) \cdot P_Y(z - x)$.

### 3. Intuição

A convolução responde:  
> "Qual é a probabilidade de que **a soma** de duas variáveis independentes assuma um valor $z$?"

Ela **varre todos os jeitos possíveis** de decompor $z$ como $x + y$, e soma as probabilidades correspondentes.


### 4. Exemplo

Seja $X, Y \in \{0,1\}$, com:

- $P_X(0) = P_X(1) = 0.5$
- $P_Y(0) = P_Y(1) = 0.5$

Então $Z = X + Y \in \{0,1,2\}$

$$
\begin{align*}
P_Z(0) &= P_X(0) \cdot P_Y(0) = 0.25 \\
P_Z(1) &= P_X(0) \cdot P_Y(1) + P_X(1) \cdot P_Y(0) = 0.25 + 0.25 = 0.5 \\
P_Z(2) &= P_X(1) \cdot P_Y(1) = 0.25
\end{align*}
$$


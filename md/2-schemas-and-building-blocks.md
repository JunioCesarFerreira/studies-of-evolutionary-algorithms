# Teoria dos Esquemas e Hipótese dos Blocos Construtivos

Os **Algoritmos Genéticos (AGs)** são métodos de busca inspirados na evolução biológica, utilizados para resolver problemas de otimização e aprendizado de máquina. Um AG mantém uma população de soluções candidatas e as evolui ao longo de gerações por meio de seleção, recombinação e mutação. Para entender seu funcionamento com rigor matemático, devemos abordar dois conceitos fundamentais: **Teoria dos Esquemas** e **Hipótese dos Blocos Construtivos**.

---

## 1. **Formalização Matemática do Algoritmo Genético**
Seja $X$ um espaço de busca, onde cada indivíduo (solução) é representado por um vetor de bits $x \in \{0,1\}^l$ de comprimento $l$. O AG opera sobre uma população de tamanho $N$, $P_t = \{ x_1, x_2, ..., x_N \}$, na geração $t$.

O processo iterativo de um AG pode ser formalizado como:

1. **Avaliação**: Cada indivíduo recebe um valor de aptidão $f: \{0,1\}^l \to \mathbb{R}$.
2. **Seleção**: Os indivíduos são escolhidos para reprodução com probabilidade proporcional à aptidão.
3. **Cruzamento**: Aplicação de operadores de recombinação para gerar novos indivíduos.
4. **Mutação**: Pequenas perturbações estocásticas nos indivíduos.
5. **Substituição**: Formação da nova geração $P_{t+1}$.

Agora, introduzimos a **Teoria dos Esquemas** e a **Hipótese dos Blocos Construtivos** para entender como AGs exploram o espaço de busca.

---

## 2. **Teoria dos Esquemas**
Um **esquema** $H$ é uma máscara que representa um subconjunto de soluções. Formalmente, um esquema é uma string de comprimento $l$ contendo elementos de $\{0,1,*\}$, onde o símbolo $*$ significa "não importa". 

Por exemplo, $H = 1*0*$ representa os indivíduos $\{1000, 1001, 1100, 1101\}$ em uma população de indivíduos com 4 bits.

### 2.1. **Ordem e Definição Formal**
Seja $\mathcal{H}$ o conjunto de todos os esquemas possíveis em $\{0,1\}^l$. Um esquema $H \in \mathcal{H}$ tem:

- **Ordem do esquema**, $o(H)$, que é o número de bits especificados (não $*$).
- **Largura do esquema**, $\delta(H)$, que é a distância entre a primeira e a última posição específica.

A quantidade de indivíduos em $P_t$ que pertence ao esquema $H$ é dada por $m(H,t)$.

---

### 2.2. **Teorema Fundamental da Teoria dos Esquemas**
A equação fundamental que descreve a dinâmica de um esquema ao longo das gerações é:

$$
m(H,t+1) \geq \frac{m(H,t) \cdot f(H)}{\bar{f}_t} \cdot (1 - p_c)^{\delta(H)} \cdot (1 - p_m)^{o(H)}
$$

onde:
- $f(H)$ é a aptidão média dos indivíduos que pertencem a $H$.
- $\bar{f}_t$ é a aptidão média da população em $t$.
- $p_c$ é a taxa de crossover.
- $p_m$ é a taxa de mutação.

Esse teorema mostra que esquemas com alta aptidão média, baixa largura $\delta(H)$ e baixa ordem $o(H)$ tendem a crescer exponencialmente ao longo das gerações.

---

## 3. **Hipótese dos Blocos Construtivos**
A **Hipótese dos Blocos Construtivos** (Building Block Hypothesis) propõe que AGs funcionam combinando **esquemas de alta aptidão e baixa ordem** em soluções cada vez melhores.

Formalmente, a hipótese afirma que:
1. Pequenos esquemas de alta aptidão (\emph{blocos construtivos}) são preservados pela seleção e reprodução.
2. O crossover os recombina de maneira progressiva para formar soluções melhores.
3. A mutação tem efeito disruptivo, mas pode introduzir diversidade para escapar de ótimos locais.

Se considerarmos que um AG mantém um conjunto de $M$ blocos construtivos $\{H_1, H_2, ..., H_M\}$, então a busca no espaço de soluções pode ser modelada como um processo de combinação probabilística desses blocos, seguindo a dinâmica imposta pelo **Teorema dos Esquemas**.

---

## 4. **Conclusão**
A Teoria dos Esquemas e a Hipótese dos Blocos Construtivos fornecem uma base teórica sólida para entender a dinâmica dos Algoritmos Genéticos. Elas mostram que a seleção favorece esquemas de alta aptidão, enquanto o crossover os recombina em soluções promissoras, promovendo um processo evolutivo eficiente.

Esses conceitos justificam a capacidade dos AGs de encontrar soluções ótimas combinando partes benéficas de diferentes indivíduos, tornando-os eficientes para problemas complexos de otimização.

---

# Espaço Contínuo

Quando os **Algoritmos Genéticos (AGs)** operam sobre variáveis reais ($\mathbb{R}$) em vez de bits ($\{0,1\}$), os conceitos fundamentais da **Teoria dos Esquemas** e da **Hipótese dos Blocos Construtivos** precisam ser adaptados, pois não há mais uma representação discreta com posições fixas. 

---

## **1. Representação em Espaço Contínuo**
Em vez de um vetor binário, cada indivíduo passa a ser um vetor de números reais:

$$
x = (x_1, x_2, \dots, x_l) \in \mathbb{R}^l
$$

onde cada alelo $x_i$ pode assumir qualquer valor dentro de um intervalo $[a_i, b_i]$. Isso significa que a busca ocorre em um espaço contínuo.

### **1.1. Definição de um Esquema no Espaço Contínuo**
No espaço binário, um esquema $H$ define uma máscara com bits fixos e curingas ($*$). Em um espaço contínuo, um esquema pode ser visto como uma **hiper-região** definida por restrições sobre cada variável:

$$
H = [a_1, b_1] \times [a_2, b_2] \times \dots \times [a_k, b_k]
$$

onde $k \leq l$ é o número de variáveis restritas. Assim, um esquema $H$ corresponde a uma região do espaço de busca em que certos parâmetros estão confinados a intervalos específicos.

A **ordem do esquema** $o(H)$ pode ser definida como o número de variáveis com restrições apertadas, e a **largura $\delta(H)$** pode ser associada à dispersão dos valores dentro desses intervalos.

---

## **2. O Teorema dos Esquemas no Espaço Contínuo**
A dinâmica dos esquemas pode ser estendida para números reais considerando aproximações contínuas. O crescimento da fração de indivíduos que pertencem a uma região $H$ pode ser modelado por:

$$
m(H,t+1) \geq \frac{m(H,t) \cdot f(H)}{\bar{f}_t} \cdot P_{c}(H) \cdot P_{m}(H)
$$

onde:
- $P_c(H)$ modela o efeito da recombinação contínua e depende do operador de crossover usado.
- $P_m(H)$ modela o efeito da mutação, que altera valores continuamente.

---

## **3. Crossover e Hipótese dos Blocos Construtivos em Espaço Contínuo**
A **Hipótese dos Blocos Construtivos** ainda se aplica, mas a recombinação ocorre de maneira diferente. Algumas estratégias incluem:

1. **Crossover de ponto médio**:
   $$
   x_{\text{filho}} = \lambda x_{\text{pai1}} + (1 - \lambda) x_{\text{pai2}}, \quad \lambda \in [0,1]
   $$
   Esse método combina informações de dois pais, mantendo os valores dentro dos intervalos.

2. **Crossover aritmético**:
   $$
   x_{\text{filho}} = \alpha x_{\text{pai1}} + (1-\alpha) x_{\text{pai2}}, \quad \alpha \in \mathbb{R}
   $$
   Onde $\alpha$ pode ser escolhido para explorar diferentes regiões do espaço de busca.

3. **Crossover BLX-$\alpha$ (Blend Crossover)**:
   Define um novo valor dentro de um intervalo expandido entre os pais:
   $$
   x_{\text{filho}} \in [\min(x_{\text{pai1}}, x_{\text{pai2}}) - \alpha d, \max(x_{\text{pai1}}, x_{\text{pai2}}) + \alpha d]
   $$
   onde $d = |x_{\text{pai1}} - x_{\text{pai2}}|$.

---

## **4. Mutação em Espaço Contínuo**
Em vez de flips de bits, a mutação no espaço contínuo envolve perturbações suaves:

- **Mutação Gaussiana**:
  $$
  x_i' = x_i + \mathcal{N}(0, \sigma^2)
  $$
  onde $\mathcal{N}(0, \sigma^2)$ é uma perturbação aleatória com distribuição normal.

- **Mutação uniforme**:
  $$
  x_i' = x_i + U(-\Delta, \Delta)
  $$
  onde $U(-\Delta, \Delta)$ é uma variável uniforme.

Essas mutações garantem que a diversidade não seja perdida e que a busca continue em regiões promissoras.

---

## **5. Conclusão**
A **Teoria dos Esquemas** e a **Hipótese dos Blocos Construtivos** podem ser generalizadas para AGs contínuos ao considerar regiões do espaço de busca em vez de padrões binários fixos. A evolução ocorre combinando soluções promissoras e explorando regiões adjacentes por meio de operadores de crossover e mutação adaptados ao espaço contínuo.

Isso permite que AGs sejam eficazes para otimização de funções sobre variáveis reais, como problemas de engenharia e aprendizado de máquina.

---

# Caso particular

Para adaptar a **Teoria dos Esquemas** e a **Hipótese dos Blocos Construtivos** ao caso contínuo com os operadores **Crossover Binário Simulado (SBX)** e **Mutação Polinomial**, devemos reformular a noção de esquemas e sua propagação ao longo das gerações.  

---  

## **1. Representação Contínua de Esquemas**  
No espaço contínuo $\mathbb{R}^l$, um **esquema** não pode mais ser definido como um padrão fixo de bits. Em vez disso, podemos modelar um esquema $H$ como uma **região do espaço de busca**, definida por restrições sobre cada variável:

$$
H = [a_1, b_1] \times [a_2, b_2] \times \dots \times [a_k, b_k]
$$

onde $k \leq l$ representa as dimensões restritas. A **ordem do esquema** $o(H)$ pode ser associada ao número de variáveis com restrições apertadas, enquanto a **largura $\delta(H)$** pode representar a dispersão dos valores dentro desses intervalos.

---  

## **2. Crossover Binário Simulado (SBX) e Teoria dos Esquemas**  
O **SBX (Simulated Binary Crossover)** é inspirado no crossover de um ponto usado em AGs binários, mas adaptado ao espaço contínuo. Ele gera filhos próximos dos pais ao imitar o comportamento de recombinação genética discreta.

### **2.1. Definição do SBX**  
Sejam dois pais $x^{(1)}$ e $x^{(2)}$, onde cada componente $x_i^{(1)}$ e $x_i^{(2)}$ é um número real. O SBX gera filhos usando a seguinte transformação:

$$
\beta_q = 
\begin{cases} 
(2u)^{\frac{1}{\eta_c + 1}}, & \text{se } u \leq 0.5 \\
\left(\frac{1}{2(1 - u)}\right)^{\frac{1}{\eta_c + 1}}, & \text{se } u > 0.5
\end{cases}
$$

onde:
- $u \sim U(0,1)$ é uma variável aleatória uniforme,
- $\eta_c$ é o **parâmetro de distribuição** que controla a proximidade dos filhos em relação aos pais.

Os filhos são então gerados como:

$$
x_i'^{(1)} = \frac{1}{2} \left[ (1 + \beta_q)x_i^{(1)} + (1 - \beta_q)x_i^{(2)} \right]
$$

$$
x_i'^{(2)} = \frac{1}{2} \left[ (1 - \beta_q)x_i^{(1)} + (1 + \beta_q)x_i^{(2)} \right]
$$

### **2.2. Impacto sobre Esquemas**  
- O SBX mantém a média dos pais e introduz pouca perturbação se $\eta_c$ for grande, favorecendo a propagação de blocos construtivos.  
- Pequenos valores de $\eta_c$ produzem filhos mais afastados, reduzindo a pressão seletiva sobre esquemas bem adaptados.  
- Esquemas com regiões estreitas (pequeno $\delta(H)$) podem ser afetados, pois filhos podem escapar da região de alta aptidão.

Assim, o SBX preserva melhor os esquemas quando $\eta_c$ é alto, garantindo que os blocos construtivos úteis sejam transmitidos às próximas gerações.

---

## **3. Mutação Polinomial e Teoria dos Esquemas**  
A **mutação polinomial** introduz pequenas variações nos indivíduos com uma distribuição ajustável pela taxa $\eta_m$.

### **3.1. Definição da Mutação Polinomial**  
A mutação ocorre aplicando a seguinte perturbação a cada gene $x_i$:

$$
\delta_i =
\begin{cases} 
(2u)^{\frac{1}{\eta_m + 1}} - 1, & \text{se } u \leq 0.5 \\
1 - \left[2(1 - u)\right]^{\frac{1}{\eta_m + 1}}, & \text{se } u > 0.5
\end{cases}
$$

onde $u \sim U(0,1)$ e $\eta_m$ controla a severidade da mutação. O novo valor do gene é então:

$$
x_i' = x_i + \delta_i (b_i - a_i)
$$

onde $b_i$ e $a_i$ são os limites do intervalo da variável.

### **3.2. Impacto sobre Esquemas**  
- Para valores altos de $\eta_m$, a mutação gera pequenas perturbações, preservando melhor os esquemas.
- Para valores baixos de $\eta_m$, grandes mudanças podem ocorrer, destruindo blocos construtivos, mas permitindo maior exploração do espaço de busca.

Portanto, a mutação polinomial desempenha um papel duplo:
1. Com $\eta_m$ alto, reforça a exploração local e mantém esquemas promissores.
2. Com $\eta_m$ baixo, ajuda na diversificação, promovendo novos blocos construtivos.

---

## **4. Conclusão**  
A combinação do **SBX** e da **Mutação Polinomial** permite uma adaptação contínua da **Hipótese dos Blocos Construtivos** e da **Teoria dos Esquemas** ao espaço de busca real. O SBX atua principalmente na **recombinação de padrões existentes**, enquanto a Mutação Polinomial **introduz variação controlada**.

A propagação de esquemas segue uma equação análoga ao Teorema dos Esquemas discreto:

$$
m(H,t+1) \geq \frac{m(H,t) \cdot f(H)}{\bar{f}_t} \cdot P_{c}(H) \cdot P_{m}(H)
$$

onde:
- $P_c(H)$ é alto para SBX com $\eta_c$ grande (preservação de padrões),
- $P_m(H)$ depende de $\eta_m$, balanceando entre **exploração** e **exploração local**.

Dessa forma, os **blocos construtivos** podem emergir e se propagar, garantindo que a busca em espaço contínuo preserve estruturas úteis e otimize funções de maneira eficiente.
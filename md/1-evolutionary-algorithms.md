# Algoritmos Evolucionários

Nesta nota, vamos formalizar matemáticamente as operações elementares e a sequência geral dos **algoritmos evolutivos (AEs)**. A definição geral inclui os principais componentes dos AEs: **população**, **avaliação**, **seleção**, **recombinação**, **mutação** e **substituição**.

---

## 1. Definições Gerais

### 1.1. Formalização de Genótipo e Fenótipo
Definimos:
1. **Cromossomo**:
   - Um **cromossomo** é uma estrutura que codifica uma solução candidata para o problema em questão. Ele pode ser representado como um vetor de elementos, onde cada elemento é um **gene**.
   - Formalmente, um cromossomo $C$ pode ser definido como:
     $$
     C = (g_1, g_2, \dots, g_n)
     $$
     onde $g_i$ representa o $i$-ésimo gene do cromossomo, e $n$ é o número total de genes no cromossomo.

2. **Gene**:
   - Um **gene** é uma unidade básica de informação no cromossomo. Cada gene $g_i$ pode assumir diferentes valores, chamados de **alelos**.
   - Formalmente, um gene $g_i$ pode ser definido como:
     $$
     g_i \in A_i
     $$
     onde $A_i$ é o conjunto de alelos possíveis para o $i$-ésimo gene.

3. **Alelo**:
   - Um **alelo** é um valor específico que um gene pode assumir. Dependendo da representação, os alelos podem ser binários (0 ou 1), inteiros, reais, ou até mesmo símbolos de um alfabeto.
   - Formalmente, um alelo $a_i$ para o $i$-ésimo gene pode ser definido como:
     $$
     a_i \in A_i
     $$
     onde $A_i$ é o conjunto de alelos possíveis para o $i$-ésimo gene.

4. **Mapeamento Genótipo-Fenótipo**
- O **genótipo** é a representação interna do cromossomo, ou seja, a codificação da solução.
- O **fenótipo** é a expressão do genótipo no contexto do problema, ou seja, a solução decodificada.
- Formalmente, o mapeamento do genótipo para o fenótipo pode ser representado por uma função $F$:
  $$
  \begin{align*}
  F: \mathcal{C} &\rightarrow \mathcal{S}\\
    C &\mapsto S
  \end{align*}
  $$
  onde $C$ é o cromossomo (genótipo) e $S$ é a solução decodificada (fenótipo).

### 1.2. População
- O conjunto $\mathcal{C}$ contém todos os cromossomos.
- Uma **população** $\mathcal{P}\subset \mathcal{C}$ é um conjunto de $n$ cromossomos (indivíduos), onde cada cromossomo $C_i$ representa uma solução candidata.
  $$
  \mathcal{P} = \{C_1, C_2, \dots, C_n\}
  $$
  Cada **cromossomo** $C_i$ é um vetor de genes:
  $$
  C_i = (g_{i1}, g_{i2}, \dots, g_{in})
  $$
  onde $g_{ij}$ é o $j$-ésimo gene do $i$-ésimo cromossomo, e $n$ é o número de genes por cromossomo.

### 1.3. Função de Avaliação (Fitness)
- A função de avaliação $\phi$ mapeia um cromossomo $C_i$ para um valor de fitness $\phi(C_i)$, que mede a qualidade da solução representada por $C_i$.
  $$
  \phi: \mathcal{C} \rightarrow \mathbb{R}^+
  $$
  O fitness é um número positivo que reflete a adequação da solução ao problema.

### 1.4. Operadores de Reprodução
- **Seleção**: Seleciona indivíduos da população atual para reprodução. A seleção é tipicamente probabilística, com indivíduos de maior fitness tendo maior chance de serem selecionados.
  $$
  \begin{align*}
    S: 2^\mathcal{C} &\rightarrow 2^\mathcal{C} \\
    \mathcal{P} &\mapsto \mathcal{P}_{\text{selecionados}}
  \end{align*}
  $$
  onde $\mathcal{P}_{\text{selecionados}}$ é um subconjunto de $\mathcal{P}$.

- **Recombinação (Crossover)**: Combina dois ou mais cromossomos selecionados para gerar descendentes. A recombinação pode ser definida como:
  $$
  \begin{align*}
    R: 2^\mathcal{C} \times 2^\mathcal{C} &\rightarrow 2^\mathcal{C} \\
    C_i \times C_j &\mapsto C_{\text{descendente}}
  \end{align*}
  $$
  onde $C_i$ e $C_j$ são cromossomos pais, e $C_{\text{descendente}}$ é o cromossomo descendente.

- **Mutação**: Modifica aleatoriamente um ou mais genes de um cromossomo. A mutação pode ser definida como:
  $$
  \begin{align*}
    M: 2^\mathcal{C} &\rightarrow 2^\mathcal{C} \\
    C_i &\mapsto C_{\text{mutado}}
  \end{align*}
  $$
  onde $C_{\text{mutado}}$ é o cromossomo resultante após a mutação.

### Substituição
- A substituição define como a nova população é formada a partir dos descendentes e da população atual. Pode ser elitista (mantendo os melhores indivíduos) ou geracional (substituindo toda a população).
  $$
  \mathcal{P}_{t+1} = \tau(\mathcal{P_t}, \mathcal{P}_{\text{descendentes}})
  $$

---

## 2. Sequência Genérica dos Algoritmos Evolutivos

A sequência genérica de um algoritmo evolutivo pode ser formalizada como um processo iterativo que segue os seguintes passos:

1. **Inicialização**:
   - Gere uma população inicial $\mathcal{P}_0$ de $N$ cromossomos aleatórios:
     $$
     \mathcal{P}_0 = \{C_1, C_2, \dots, C_N\}
     $$
     onde cada $C_i$ é gerado aleatoriamente.

2. **Avaliação**:
   - Calcule o fitness de cada cromossomo na população:
     $$
     \phi(C_i) \quad \forall C_i \in \mathcal{P}_t
     $$
     onde $\mathcal{P}_t$ é a população na geração $t$.

3. **Condição de Parada**:
   - Verifique se a condição de parada foi atingida (por exemplo, número máximo de gerações ou fitness desejado). Se sim, retorne a melhor solução encontrada.

4. **Seleção**:
   - Selecione $k$ cromossomos da população atual para reprodução:
     $$
     \mathcal{P}_{\text{selecionados}} = S(\mathcal{P}_t)
     $$

5. **Recombinação**:
   - Aplique o operador de recombinação para gerar descendentes:
     $$
     \mathcal{P}_{\text{descendentes}} = \{R(C_i, C_j) \mid C_i, C_j \in \mathcal{P}_{\text{selecionados}}\}
     $$

6. **Mutação**:
   - Aplique o operador de mutação aos descendentes:
     $$
     \mathcal{P}_{\text{mutados}} = \{M(C_i) \mid C_i \in \mathcal{P}_{\text{descendentes}}\}
     $$

7. **Substituição**:
   - Forme a nova população $\mathcal{P}_{t+1}$ combinando a população atual e os descendentes mutados:
     $$
     \mathcal{P}_{t+1} = \text{Substituição}(\mathcal{P}_t, \mathcal{P}_{\text{mutados}})
     $$

8. **Iteração**:
   - Incremente $t$ e retorne ao passo 2.

---

## 3. Pseudocódigo Formal

A sequência genérica pode ser resumida no seguinte pseudocódigo:

1. Inicialize a população $\mathcal{P}_0$ com $N$ cromossomos aleatórios.
2. Avalie o fitness $\phi(C_i)$ para cada $C_i \in \mathcal{P}_t$.
3. Enquanto a condição de parada não for satisfeita:
    1. Selecione $\mathcal{P}_{\text{selecionados}} = S(\mathcal{P}_t)$.
    2. Recombine $\mathcal{P}_{\text{descendentes}} = \{R(C_i, C_j) \mid C_i, C_j \in \mathcal{P}_{\text{selecionados}}\}$.
    3. Mute $\mathcal{P}_{\text{mutados}} = \{M(C_i) \mid C_i \in \mathcal{P}_{\text{descendentes}}\}$.
    4. Substitua $\mathcal{P}_{t+1} = \text{Substituição}(\mathcal{P}_t, \mathcal{P}_{\text{mutados}})$.
    5. Avalie o fitness $\phi(C_i)$ para cada $C_i \in \mathcal{P}_{t+1}$.
    6. Incremente $t$.
4. Retorne a melhor solução encontrada.

---
# KNN — k-Nearest Neighbors

## O que é o KNN

<details>
<summary><strong>O que é o KNN</strong></summary>

O **k-Nearest Neighbors (k-Vizinhos Mais Próximos)** é um dos algoritmos mais simples de Machine Learning.

Ele é usado tanto para **classificação** quanto para **regressão**, e funciona com base na **proximidade** entre os dados.

Ideia central:

> Quando queremos prever algo novo, o algoritmo procura os “k” exemplos mais parecidos no conjunto de treino e usa as respostas deles para decidir o resultado.
> 

Por isso o nome “k-vizinhos mais próximos”.
</details>

---

<details>
<summary><strong>Como o KNN funciona</strong></summary>

## Como o KNN funciona

1. **Guardar os dados**
    
    Diferente de outros modelos, o KNN não aprende uma função matemática.
    
    Ele apenas **armazena** todos os exemplos do conjunto de treino.
    
2. **Calcular as distâncias**
    
    Quando chega um novo dado para classificar ou prever, o KNN mede **a distância entre esse novo ponto e todos os pontos já conhecidos**.
    
    As distâncias podem ser calculadas de várias formas (a mais comum é a distância Euclidiana).
    
    Fórmula da distância Euclidiana entre dois pontos A e B:
    
    $$
    
    d(A,B) = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}
    
    $$
    
3. **Selecionar os k vizinhos mais próximos**
    
    Depois de calcular todas as distâncias, o algoritmo pega os **k menores valores,** ou seja, os vizinhos mais próximos do ponto que queremos prever.
    
4. **Decidir a resposta**
    - **Para classificação:** o KNN escolhe a **classe mais comum** entre os vizinhos.
    (Exemplo: se dos 5 vizinhos, 3 são da classe A e 2 são da classe B, o resultado é A.)
    - **Para regressão:** o KNN tira a **média** dos valores dos vizinhos.
</details>

---

<details>
<summary><strong>Exemplo prático</strong></summary>

## Exemplo prático

Um modelo que tenta prever o tipo de fruta com base em duas características: peso e textura.

Quando inserimos uma nova fruta, o KNN vai:

1. Calcular a distância dela para todas as frutas conhecidas.
2. Pegar as 3 mais próximas (por exemplo, `k = 3`).
3. Ver quais classes aparecem com mais frequência entre essas 3 frutas.
4. Classificar a nova fruta como a classe predominante.
</details>

---

<details>
<summary><strong>Escolha do valor de k</strong></summary>

## Escolha do valor de k

O valor de k é um dos fatores mais importantes para o desempenho do KNN.

- Um k pequeno (como 1 ou 2) pode deixar o modelo muito sensível a ruídos e outliers.
- Um k muito grande pode deixar o modelo genérico demais, ignorando detalhes importantes.

Em geral, o valor de k é escolhido com base em experimentos com o conjunto de validação.
</details>

---

<details>
<summary><strong>Tipos de distância</strong></summary>

## Tipos de distância

O KNN pode usar diferentes maneiras de calcular o que significa “estar próximo”.

As principais são:

| Tipo de Distância | Descrição | Exemplo |
| --- | --- | --- |
| **Euclidiana** | Distância em linha reta entre dois pontos. | Caminho direto. |
| **Manhattan** | Distância somando os deslocamentos horizontais e verticais. | Como andar em ruas de um quarteirão. |
| **Chebyshev** | Considera apenas o maior deslocamento em qualquer dimensão. | Movimento de uma torre no xadrez. |

A escolha da métrica depende do tipo de dado e da relação entre as variáveis.
</details>

---

<details>
<summary><strong>Vantagens e desvantagens</strong></summary>

## Vantagens e desvantagens

### Vantagens

- Simples de entender e implementar.
- Não precisa de treinamento.
- Funciona bem com dados pequenos e bem distribuídos.

### Desvantagens

- Fica lento com muitos dados, pois precisa comparar o novo ponto com todos os outros.
- Depende fortemente da escala das variáveis (é importante normalizar os dados).
- Pode se confundir com dados muito ruidosos ou com classes desbalanceadas.
</details>

---

<details>
<summary><strong>Quando usar o KNN</strong></summary>

## Quando usar o KNN

O KNN é bom para:

- Problemas simples de classificação, onde os dados têm poucas dimensões.
- Casos onde os padrões são bem definidos (como imagens pequenas, dados médicos, ou datasets de treino organizados).

Mas não é quando:

- O conjunto de dados é muito grande (fica lento).
- Existem muitas variáveis.
- As classes têm tamanhos muito diferentes.
</details>

---

<details>
<summary><strong>Exemplo de código prático</strong></summary>

## Exemplo de código prático

O algoritmo KNN foi implementado e testado em meus experimentos no repositório de Machine Learning,

na seção de **Foundations → Notebooks**, que cobre exemplos do livro *Introduction to Machine Learning with Python*.

🔗 Veja a implementação completa:
[Repositório Machine Learning Labs — Foundations (KNN)](https://github.com/Xandetds/machine-learning-labs/tree/main/0_FOUNDATIONS/notebooks)

Abaixo, um exemplo resumido de como o algoritmo é implementado com a biblioteca `scikit-learn`:

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score

# Carregar o dataset
X, y = load_iris(return_X_y=True)

# Dividir em treino e teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=42)

# Criar o modelo com k=3
model = KNeighborsClassifier(n_neighbors=3)

# Treinar e prever
model.fit(X_train, y_train)
pred = model.predict(X_test)

# Avaliar
print("Acurácia:", accuracy_score(y_test, pred))

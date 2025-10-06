# Conceitos gerais

Machine Learning  é uma área da inteligência artificial que ensina os computadores a aprenderem padrões a partir de dados, usando algoritmos.

Em vez de programar cada regra manualmente, damos ao computador exemplos e ele aprende a generalizar — ou seja, a identificar padrões e fazer previsões.

Por exemplo, podemos mostrar várias fotos de gatos e cachorros.

Com base nas características das imagens (como cor, forma, orelhas etc.), o modelo aprende a diferenciar um gato de um cachorro, mesmo em imagens que nunca viu antes.

## Tipos de ML

### Aprendizado Supervisionado

O modelo aprende com **dados rotulados**, ou seja, exemplos que já têm a resposta certa.

Ele recebe exemplos de entrada (x) e de saída (y), e aprende com eles.

Exemplo:

Queremos prever o preço de casas.

Para isso, daremos ao modelo dados com o tamanho da casa, número de quartos, localização, etc., junto com o preço real de cada casa.

Assim, ele aprende a relacionar as características com o preço.

### Aprendizado Não Supervisionado

O modelo aprende **sem respostas prontas**, ou seja, sem rótulos, recebendo somente a entrada (x).

Ele tenta encontrar padrões ou fazer grupos dentro dos dados.

Exemplo:

Temos dados de clientes de uma loja, mas não sabemos nada sobre eles.

O algoritmo pode agrupar clientes com comportamentos parecidos como “clientes que compram muito” ou “clientes que compram só em promoções”.

---

## Como o Computador Enxerga os Dados

Normalmente, os dados são organizados em formato de tabela:

- Cada **linha** representa uma **amostra** (um item observado, como uma casa, um cliente, uma flor).
- Cada coluna representa uma característica/feature dessa amostra, como preço, cor, peso, etc.
- Cada valor da tabela é uma medida ou atributo usado pelo modelo.

Exemplo onde o tamanho e os quartos são o x, e o preço é o y, ou seja, o dado em que a máquina vai prever.

| Tamanho (m²) | Quartos | Preço (R$) |
| --- | --- | --- |
| 80 | 2 | 350.000 |
| 120 | 3 | 500.000 |
| 200 | 4 | 750.000 |

---

## Divisão do Conjunto de Dados

Antes de treinar o modelo, normalmente dividimos o conjunto de dados em duas partes:

- **Treino (training set)**: usado para o modelo aprender.
- **Teste (test set)**: usado para ver se o modelo aprendeu bem.

Isso ajuda a evitar que o modelo apenas “memorize” os exemplos, e garante que ele saiba generalizar para novos dados.

---

## Métricas Básicas de Avaliação

Algumas formas comuns de avaliar o desempenho de um modelo são:

- Acurácia (Accuracy) – percentual de acertos do modelo.
- Erro Médio Quadrático (MSE) – mede o quanto as previsões diferem dos valores reais.
- R² (Coeficiente de Determinação) – indica quanto da variação dos dados o modelo consegue explicar.
# Regressão vs Classificação

## Diferença entre Regressão e Classificação

No Machine Learning, o tipo de problema depende do que queremos prever.

<details>
<summary><strong>Regressão</strong></summary>

### Regressão

Usada quando o objetivo é **prever um valor numérico contínuo**.

Exemplo: prever o preço de um produto, a temperatura de amanhã ou a altura de uma pessoa.

Características:

- O resultado é um **número real**.
- Os erros são medidos por métricas como **MSE (Mean Squared Error)** e **R²**.
- Pequenas diferenças são aceitáveis (por exemplo, prever R$ 498.000 em vez de R$ 500.000).
</details>

---

<details>
<summary><strong>Classificação</strong></summary>

### Classificação

Usada quando o objetivo é **atribuir uma categoria** ou **classe** a cada exemplo.

Exemplo: identificar se um e-mail é “spam” ou “não spam”, ou prever o tipo de flor ou a raça de um cachorro.

Características:

- O resultado é **uma classe** (rótulo).
- Avaliada com métricas como **acurácia**, **precisão** e **recall**.
- Pequenas diferenças **não são aceitáveis** (um erro muda completamente a classe).
</details>

---

<details>
<summary><strong>Exemplos Práticos</strong></summary>

## Exemplos Práticos

| Tipo de Problema | Exemplo | Tipo de Saída |
| --- | --- | --- |
| Regressão | Prever o preço de uma casa | Valor numérico |
| Classificação | Identificar se um e-mail é spam | Categoria (“spam” / “não spam”) |
| Regressão | Prever a idade de uma pessoa | Valor numérico |
| Classificação | Determinar o tipo de animal em uma foto | Categoria (“gato”, “cachorro”) |
</details>

---

<details>
<summary><strong>Como Saber Qual Tipo Usar</strong></summary>

## Como Saber Qual Tipo Usar

1. Se o resultado for um número contínuo, use Regressão.
2. Se o resultado for uma categoria, use Classificação.
3. Se o problema envolver agrupamentos automáticos, sem resposta certa, use Aprendizado Não Supervisionado.
</details>

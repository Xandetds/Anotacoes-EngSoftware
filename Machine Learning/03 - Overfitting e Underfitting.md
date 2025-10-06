# Overfitting e Underfitting

## Conceitos

Um dos desafios do Machine Learning é equilibrar a complexidade do modelo.

Se o modelo for simples demais, ele não aprende o suficiente.

Se for complexo demais, ele decora os dados.

## Underfitting (Subajuste)

Acontece quando o modelo é **simples demais** para capturar os padrões dos dados.

Ele não aprende bem nem nos dados de treino.

Sintomas:

- Baixa performance tanto no treino quanto no teste.
- O modelo não consegue representar a relação entre as variáveis.

Exemplo:

Tentar ajustar uma **reta** simples a dados que claramente seguem uma curva.

---

## Overfitting (Sobreajuste)

Acontece quando o modelo é **complexo demais**.

Ele aprende os detalhes e ruídos do conjunto de treino, mas não generaliza bem.

Sintomas:

- Excelente performance no treino.
- Fraco desempenho no teste (erros grandes em novos dados).

Exemplo:

Criar uma função super detalhada que passa exatamente por todos os pontos do treino, mas falha completamente ao prever novos exemplos.

---

## Equilíbrio Ideal

O objetivo é encontrar um modelo que:

- Aprenda bem os padrões reais (sem decorar).
- Generalize bem para dados novos.

Esse equilíbrio é o que diferencia um modelo útil de um modelo que só funciona na teoria

---

## Exemplo de Visualização

Tem três curvas representando modelos diferentes:

1. **Underfitting:** uma linha reta que não acompanha os dados.
2. **Bom ajuste:** uma curva suave que segue a tendência geral.
3. **Overfitting:** uma curva que passa exatamente por todos os pontos.

O bom modelo está entre os dois extremos.

---

## Estratégias para Evitar Overfitting

- Ter mais dados de treino (para o modelo aprender melhor padrões reais).
- Simplificar o modelo (menos parâmetros).
- Usar regularização (penaliza complexidade excessiva).
- Aplicar validação cruzada (cross-validation).
- Parar o treino no momento certo (early stopping), em redes neurais.
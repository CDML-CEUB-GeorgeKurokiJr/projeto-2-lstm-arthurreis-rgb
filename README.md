# 📈 Previsão de Direção de Ações Bancárias com LSTM (Deep Learning)

## 📌 Objetivo

Este projeto tem como objetivo prever a **direção do preço (alta ou queda)** de ações bancárias brasileiras utilizando **Redes Neurais Recorrentes (LSTM)**.

Ao invés de prever valores exatos, o modelo resolve um problema de **classificação binária**, indicando:

* **1 → o preço irá subir**
* **0 → o preço irá cair**

---

## 🧠 Premissa do Projeto

O mercado financeiro é altamente complexo e ruidoso, tornando previsões exatas de preços extremamente difíceis.

Dessa forma, adotamos a seguinte premissa:

> É mais eficiente prever a **direção do movimento** (sobe/cai) do que o valor exato do preço.

Além disso:

* Utilizamos múltiplos ativos do mesmo setor (bancos)
* O modelo aprende padrões temporais com LSTM
* A previsão considera um horizonte de **5 dias à frente**

---

## 📊 Dados Utilizados

Dados obtidos via Yahoo Finance utilizando a biblioteca `yfinance`.

### Ativos analisados:

* ITUB4 (Itaú)
* BBDC4 (Bradesco)
* BBAS3 (Banco do Brasil)
* SANB11 (Santander)

### Período:

* **Treino:** 2010 – 2017
* **Teste:** 2018

Separação temporal respeitada para evitar vazamento de dados.

---

## ⚙️ Engenharia de Features

Foram utilizadas features relevantes para séries financeiras:

* Retornos (1 e 5 dias)
* Momentum (diferença de preço)
* Relações entre ativos (spreads entre bancos)

Essas variáveis permitem capturar:

* Tendência de mercado
* Força de movimento
* Correlação entre ativos do mesmo setor

---

## 🎯 Target (Variável Alvo)

A variável alvo é definida como:

* Soma dos retornos dos próximos **5 dias**
* Convertida em classificação binária:

```
1 → preço sobe
0 → preço cai
```

---

## 🤖 Modelo

Modelo baseado em **LSTM (Long Short-Term Memory)**:

* 2 camadas LSTM
* 128 unidades ocultas
* Dropout para evitar overfitting
* Camada final com **4 saídas (uma por banco)**
* Função Sigmoid para gerar probabilidades

Tipo:

> Classificação multi-output (multi-tarefa)

---

## 🏋️ Treinamento

* Loss: Binary Cross Entropy (BCE)
* Otimizador: Adam
* Batch size: 32
* Janela temporal: 30 dias

---

## 📊 Avaliação

A métrica principal utilizada foi:

* **Acurácia direcional (%)**

O modelo supera o baseline aleatório (50%), indicando aprendizado de padrões.

---

## 📊 Resultados Obtidos

### 🏦 Itaú (ITUB4)

* Acurácia: **65.83%**
* Precisão: **40.00%**
* Recall: **18.67%**
* F1-Score: **25.45%**

---

### 🏦 Bradesco (BBDC4)

* Acurácia: **57.92%**
* Precisão: **31.11%**
* Recall: **16.67%**
* F1-Score: **21.71%**

---

### 🏦 Banco do Brasil (BBAS3)

* Acurácia: **56.25%**
* Precisão: **44.78%**
* Recall: **30.61%**
* F1-Score: **36.36%**

---

### 🏦 Santander (SANB11)

* Acurácia: **60.83%**
* Precisão: **39.58%**
* Recall: **22.62%**
* F1-Score: **28.79%**

---

## 📈 Interpretação dos Gráficos

O projeto gera gráficos de **Real vs Previsto** para cada ação, onde:

* Linha sólida → valor real (0 ou 1)
* Linha tracejada → previsão do modelo

### 🔍 Como interpretar:

* Quando as linhas estão **alinhadas**, o modelo acertou a direção do movimento
* Quando divergem, o modelo errou a previsão

### 📌 Observações importantes:

* O modelo consegue capturar **padrões de tendência**, acertando sequências consecutivas
* Existem erros em regiões mais voláteis, o que é esperado no mercado financeiro
* Alguns ativos apresentam melhor desempenho que outros, indicando:

  * Diferença de previsibilidade entre ações
  * Impacto da correlação entre os bancos

### 🎯 Conclusão visual:

Mesmo com ruído do mercado, o modelo apresenta uma capacidade consistente de prever a direção, superando o comportamento aleatório.

---

## 🚀 Possíveis Melhorias

* Walk-forward validation (validação temporal mais robusta)
* Inclusão de dados macroeconômicos
* Uso de mecanismos de atenção (Attention)
* Backtesting de estratégia de investimento

---

## 👨‍💻 Autor

Arthur Gonçalves
Estudante de Ciência de Dados e Machine Learning

---

## 📌 Conclusão

O modelo conseguiu aprender padrões temporais e relações entre ativos do setor bancário.

A abordagem de classificação binária mostrou-se mais robusta que regressão de preços, sendo mais aplicável em cenários reais de tomada de decisão.

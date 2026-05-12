# Projeto de Machine Learning — Previsão de Churn

## Descrição do Projeto

Este projeto tem como objetivo desenvolver modelos de Machine Learning capazes de prever a probabilidade de churn de usuários a partir de variáveis comportamentais e históricas.

O trabalho foi desenvolvido utilizando a metodologia SEMMA:

- Sample
- Explore
- Modify
- Model
- Assess

Foram utilizados modelos supervisionados para classificação binária, com foco na identificação de usuários com maior risco de evasão.

---

# Objetivo

Construir modelos capazes de:

- prever churn de usuários;
- estimar probabilidades de churn;
- priorizar usuários com maior risco;
- avaliar ganhos operacionais através de métricas de lift e churn capturado.

---

# Estrutura do Projeto

```text
.
├── dados/
├── notebooks/
├── modelos/
├── README.md
└── Previsão_de_Churn.ipynb
```

---

# Metodologia

## 1. Sample

Foi realizado o particionamento temporal da base.

- O último mês foi separado como base OOT (Out Of Time), simulando dados futuros.
- O restante da base foi dividido em:
  - 80% treino
  - 20% teste

---

## 2. Explore

Nesta etapa foram realizadas análises exploratórias dos dados, incluindo:

- análise das variáveis numéricas;
- análise da variável alvo;
- identificação de distribuição das classes;
- análise de comportamento temporal;
- verificação de possíveis padrões de churn.

---

## 3. Modify

Foi utilizado Pipeline e ColumnTransformer da biblioteca scikit-learn para padronizar o fluxo de transformação dos dados.

### Tratamentos realizados

- remoção de colunas não utilizadas;
- aplicação de StandardScaler para modelos lineares;
- separação entre variáveis numéricas e categóricas;
- aplicação automática do pipeline em treino, teste e OOT.

---

## 4. Model

Foram treinados os seguintes modelos:

### Regressão Logística

Modelo linear utilizado para classificação binária.

### Random Forest

Modelo baseado em ensemble de árvores de decisão.

---

# Ajuste de Hiperparâmetros

Foi utilizado GridSearchCV para busca de hiperparâmetros.

## Regressão Logística

Parâmetros ajustados:

- C
- penalty
- solver
- class_weight

## Random Forest

Parâmetros ajustados:

- n_estimators
- max_depth
- min_samples_leaf

---

# Métricas Utilizadas

## ROC AUC

Métrica principal utilizada para avaliação da capacidade de separação entre churners e não churners.

## Accuracy

Utilizada como métrica complementar.

## Lift

Utilizada para avaliar o ganho do modelo em relação a uma seleção aleatória.

## Churn Capturado

Avalia o percentual de churners identificados entre os usuários de maior risco.

---

# Resultados

## ROC AUC

| Modelo | Treino | Teste | OOT |
|---|---|---|---|
| Random Forest | 0.8438 | 0.8167 | 0.8435 |
| Regressão Logística | 0.8179 | 0.8167 | 0.8390 |

---

## Accuracy

| Modelo | Treino | Teste | OOT |
|---|---|---|---|
| Random Forest | 0.7614 | 0.7366 | 0.7745 |
| Regressão Logística | 0.7411 | 0.7281 | 0.7759 |

---

## Lift e Churn Capturado

### Random Forest

| Percentual da Base | Churn Capturado | Lift |
|---|---|---|
| 10% | 18.16% | 1.82 |
| 20% | 34.94% | 1.75 |
| 30% | 49.20% | 1.64 |

### Regressão Logística

| Percentual da Base | Churn Capturado | Lift |
|---|---|---|
| 10% | 17.93% | 1.79 |
| 20% | 34.48% | 1.72 |
| 30% | 50.34% | 1.68 |

---

# Interpretação dos Resultados

Os modelos apresentaram boa capacidade de generalização, mantendo desempenho consistente entre treino, teste e OOT.

O Random Forest apresentou melhor desempenho nos grupos de maior risco, enquanto a Regressão Logística apresentou comportamento semelhante e maior simplicidade interpretativa.

A análise de lift demonstrou que os modelos conseguem priorizar usuários com maior probabilidade de churn, obtendo desempenho superior a uma seleção aleatória.

---

# Persistência do Modelo

O modelo final foi salvo utilizando serialização via pickle.

O pipeline completo foi persistido juntamente com o modelo, permitindo:

- reutilização futura;
- inferência em produção;
- aplicação automática das transformações.

## Exemplo

```python
import pickle

with open('modelo_churn.pkl', 'wb') as f:
    pickle.dump(modelo_final, f)
```

---

# Tecnologias Utilizadas

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Pickle

---

# Possíveis Melhorias Futuras

- inclusão de novas variáveis temporais;
- engenharia de atributos de tendência;
- análise SHAP;
- calibragem de probabilidades;
- utilização de modelos boosting;
- deployment via API.

---

# Autor

Mateus


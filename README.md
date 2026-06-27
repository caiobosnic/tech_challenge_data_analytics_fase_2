# Tech Challenge Fase 2 — Classificação de Qualidade de Vinhos com Machine Learning

**PosTech FIAP — Data Analytics | Grupo 21**

> Utilizando dados físico-químicos para prever a qualidade de vinhos e apoiar decisões no processo produtivo.

---

## Objetivo

Desenvolver um modelo de classificação capaz de prever a qualidade de um vinho com base em suas características físico-químicas. A variável `quality` foi transformada em classificação binária:

- **Alta Qualidade (1):** nota ≥ 7
- **Baixa/Média Qualidade (0):** nota < 7

---

## Sobre o Dataset

- **Fonte:** [Wine Quality Dataset — Kaggle](https://www.kaggle.com/datasets/yasserh/wine-quality-dataset)
- **Arquivo:** `WineQT.csv` — 1.143 amostras de vinho tinto
- **Features:** 11 características físico-químicas + variável alvo `quality`

| Feature | Descrição |
|---|---|
| fixed acidity | Acidez fixa |
| volatile acidity | Acidez volátil — nível alto indica sabor de vinagre |
| citric acid | Ácido cítrico — frescor e sabor |
| residual sugar | Açúcar residual após fermentação |
| chlorides | Cloretos (cloreto de sódio) |
| free sulfur dioxide | SO₂ livre — preservação contra oxidação |
| total sulfur dioxide | SO₂ total |
| density | Densidade — influenciada por açúcar e álcool |
| pH | Nível de acidez |
| sulphates | Sulfatos — preservação e características sensoriais |
| alcohol | Teor alcoólico |
| **quality** | **Nota 0–10 atribuída por especialistas (variável alvo)** |

> `WineQT.csv` disponível em `data/raw/` ✅

---

## Pipeline do Projeto

### 1. Compreensão do Problema (Alexandre + Allison)
- Contexto da indústria vitivinícola
- Definição da variável alvo e binarização
- `quality_bin = 1 se quality ≥ 7, senão 0`

### 2. Análise Exploratória de Dados — EDA (Alexandre)
- Distribuição das variáveis e correlações
- Detecção de outliers via IQR: `residual_sugar` (9.6%) e `chlorides` (6.7%) com maior incidência
- Balanceamento: **984 Baixa/Média (86.1%) vs 159 Alta (13.9%)** → base desbalanceada
- Principais correlações com `quality`: `alcohol` ↑ e `volatile_acidity` ↓
- Gráficos gerados em `results/`

### 3. Pré-processamento — ETL (Allison)
- Zero valores nulos encontrados
- Binarização: `quality_bin = 1 se quality ≥ 7, senão 0`
- Exportação do `dataset_tratado.csv` em `data/processed/`

### 4. Modelos de ML — KNN e Decision Tree (Gusthavo)
- K-Nearest Neighbors
- Decision Tree
- Métricas de avaliação

### 5. Modelos de ML — Random Forest e SVM (Caio)
- Random Forest com GridSearchCV (54 combinações, 5-fold estratificado)
- SVM com kernel RBF e `probability=True` para curva ROC
- SMOTE aplicado antes do split para balancear [984, 159] → [984, 984]
- Comparativo final dos 4 modelos (DT, KNN, RF, SVM) com Accuracy, F1 e AUC-ROC

---

## Estrutura do Repositório

```
tech_challenge_data_analytics_2/
│
├── data/
│   ├── raw/
│   │   └── WineQT.csv                       # Dataset original ✅
│   └── processed/
│       └── dataset_tratado.csv              # Dataset pós-ETL com quality_bin ✅
│
├── notebooks/
│   ├── 01_EDA_Alexandre.ipynb               # EDA — Alexandre Amorim ✅
│   ├── 02_EDA_ETL_Allison.ipynb             # ETL — Allison Lima ✅
│   ├── 03_ML_Gusthavo_Soares.ipynb          # KNN + Decision Tree — Gusthavo ✅
│   └── 04_ML_Caio_Bosnic.ipynb              # Random Forest + SVM — Caio ✅
│
├── src/                                     # Scripts auxiliares
├── results/
│   ├── 01_distribuicao_features.png         # Histogramas ✅
│   ├── 02_boxplots_outliers.png             # Boxplots ✅
│   ├── 03_balanceamento_classes.png         # Desbalanceamento ✅
│   ├── 04_heatmap_correlacao.png            # Correlações ✅
│   ├── 05_scatter_features_relevantes.png  # Alcohol + Volatile Acidity ✅
│   ├── 06_cm_random_forest.png             # Matriz de Confusão RF ✅
│   ├── 07_feature_importance_rf.png        # Importância de Features RF ✅
│   ├── 08_cm_svm.png                       # Matriz de Confusão SVM ✅
│   ├── 09_roc_comparativo.png             # Curva ROC — 4 modelos ✅
│   └── 10_comparativo_metricas.png        # Comparativo Accuracy/F1/AUC ✅
├── requirements.txt
└── README.md
```

---

## Executar no Google Colab

| Notebook | Responsável | Link |
|---|---|---|
| EDA | Alexandre Amorim | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/caiobosnic/tech_challenge_data_analytics_caio/blob/main/notebooks/01_EDA_Alexandre.ipynb) |
| ETL | Allison Lima | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/caiobosnic/tech_challenge_data_analytics_caio/blob/main/notebooks/02_EDA_ETL_Allison.ipynb) |
| KNN + Decision Tree | Gusthavo Soares | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/caiobosnic/tech_challenge_data_analytics_fase_2/blob/main/notebooks/03_ML_Gusthavo_Soares.ipynb) |
| Random Forest + SVM | Caio Bosnic | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/caiobosnic/tech_challenge_data_analytics_fase_2/blob/main/notebooks/04_ML_Caio_Bosnic.ipynb) |

---

## Como Executar Localmente

```bash
git clone https://github.com/caiobosnic/tech_challenge_data_analytics_fase_2.git
cd tech_challenge_data_analytics_fase_2
pip install -r requirements.txt
jupyter notebook
```

**Ordem de execução:**
1. `01_EDA_Alexandre.ipynb`
2. `02_EDA_ETL_Allison.ipynb`
3. `03_ML_Gusthavo_Soares.ipynb`
4. `04_ML_Caio_Bosnic.ipynb`

---

## Entregáveis

| Entregável | Link |
|---|---|
| Repositório GitHub | [tech_challenge_data_analytics_fase_2](https://github.com/caiobosnic/tech_challenge_data_analytics_fase_2) |
| Apresentação Executiva (PPT/PDF) | *(adicionar no repositório em `results/`)* |
| Vídeo Executivo (≤ 5 min) | *(adicionar link)* |

---

## Autores

| Nome | RM | Contribuição |
|---|---|---|
| Alexandre de Souza Amorim | 372077 | EDA — Análise Exploratória |
| Allison Lima | 372648 | ETL — Pré-processamento |
| Caio Rodrigues Bosnic Barbosa | 372603 | ML — Random Forest + SVM |
| Gusthavo Lourenço Rios Soares | 371911 | ML — KNN + Decision Tree |

**FIAP — Pós-Tech em Data Analytics | Fase 2**

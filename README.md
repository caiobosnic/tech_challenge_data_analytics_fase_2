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

> Baixe o `WineQT.csv` no link acima e coloque em `data/raw/`.

---

## Pipeline do Projeto

### 1. Compreensão do Problema (Alexandre + Allison)
- Contexto da indústria vitivinícola
- Definição da variável alvo e binarização
- `quality_bin = 1 se quality ≥ 7, senão 0`

### 2. Análise Exploratória de Dados — EDA (Alexandre)
- Distribuição das variáveis e correlações
- Detecção de outliers (IQR)
- Análise de balanceamento: **984 (Baixa/Média) vs 159 (Alta)** → base desbalanceada
- Principais correlações: `alcohol` ↑ e `volatile_acidity` ↓

### 3. Pré-processamento — ETL (Allison)
- Tratamento de dados faltantes e padronização
- Normalização de variáveis numéricas
- Exportação do `dataset_tratado.csv`

### 4. Modelos de ML — KNN e Decision Tree (Gusthavo)
- K-Nearest Neighbors
- Decision Tree
- Métricas de avaliação

### 5. Modelos de ML — Random Forest e SVM (Caio) ← *a fazer*
- Random Forest com GridSearchCV
- SVM com `probability=True` para ROC
- SMOTE para desbalanceamento
- Comparativo de modelos com ROC/AUC

---

## Estrutura do Repositório

```
tech_challenge_data_analytics_2/
│
├── data/
│   ├── raw/
│   │   └── WineQT.csv              # Baixar do Kaggle (link acima)
│   └── processed/
│       └── dataset_tratado.csv     # Pós-ETL (Allison)
│
├── notebooks/
│   ├── 01_EDA_Alexandre.ipynb      # EDA — Alexandre Amorim
│   ├── 02_EDA_ETL_Allison.ipynb    # ETL — Allison Lima
│   ├── 03_ML_Gusthavo_Soares.ipynb # KNN + Decision Tree — Gusthavo (baixar do Colab)
│   └── 04_ML_Caio_Bosnic.ipynb     # Random Forest + SVM — Caio (a fazer)
│
├── src/                            # Scripts auxiliares
├── results/                        # Gráficos e métricas dos modelos
├── requirements.txt
└── README.md
```

---

## Executar no Google Colab

| Notebook | Responsável | Link |
|---|---|---|
| EDA | Alexandre Amorim | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/caiobosnic/tech_challenge_data_analytics_caio/blob/main/notebooks/01_EDA_Alexandre.ipynb) |
| ETL | Allison Lima | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/caiobosnic/tech_challenge_data_analytics_caio/blob/main/notebooks/02_EDA_ETL_Allison.ipynb) |
| KNN + Decision Tree | Gusthavo Soares | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1pbpeeaBWaDZ-gIBZTdMuuoYVcpb8PxDc?usp=sharing) |
| Random Forest + SVM | Caio Bosnic | *(a fazer)* |

---

## Como Executar Localmente

```bash
git clone https://github.com/caiobosnic/tech_challenge_data_analytics_caio.git
cd tech_challenge_data_analytics_caio
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
| Repositório GitHub | [tech_challenge_data_analytics_caio](https://github.com/caiobosnic/tech_challenge_data_analytics_caio) |
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

# 🎯 Customer Segmentation Prediction Platform

> Plataforma de segmentação e predição de churn para e-commerce — do dado bruto ao app interativo.

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.x-orange)
![Streamlit](https://img.shields.io/badge/Streamlit-1.x-red)
![Status](https://img.shields.io/badge/Status-Concluído-green)

> *Abra o Projeto Online clicando no botão abaixo:*

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://customer-segmentation-platform.streamlit.app/)


## 📌 Sobre o projeto

Este projeto constrói uma plataforma completa de inteligência de clientes para e-commerce, capaz de:

- **Segmentar clientes** automaticamente em 4 perfis comportamentais (VIP, Promissor, Em Risco, Perdido)
- **Predizer churn** com 98% de acurácia e ROC-AUC de 0.9993
- **Recomendar estratégias** de vendas personalizadas por segmento
- **Rodar como pipeline** que se atualiza com novos dados

---

## 🗂️ Dataset

**UCI Online Retail II** — ~1 milhão de transações reais de e-commerce britânico (2009–2011)

| Atributo | Detalhe |
|----------|---------|
| Fonte | [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/502/online+retail+ii) |
| Volume | 1.067.371 transações brutas → 770.715 após limpeza |
| Clientes | 5.816 clientes únicos identificados |
| Período | Dezembro/2009 a Dezembro/2011 |

---

## 🧠 Metodologia

### 1. EDA — Exploração dos Dados
Análise minuciosa com 22 etapas identificando problemas críticos e insights de negócio:
- 22,77% de Customer IDs nulos
- Cancelamentos, ajustes contábeis e StockCodes não-produto
- Sazonalidade clara com pico em Novembro
- Negócio B2B confirmado — compras concentradas às Quintas entre 10h e 14h

### 2. Preprocessing / ETL
Pipeline de limpeza documentado e rastreável:

| Etapa | Registros removidos |
|-------|-------------------|
| Duplicatas | 34.335 |
| Cancelamentos | 19.104 |
| StockCodes não-produto | 4.513 |
| Customer ID nulos | 226.843 |
| Outliers de Quantity | 5.868 |
| **Total removido** | **296.656 (27,79%)** |

### 3. Feature Engineering — RFM
Cálculo das 3 métricas que definem o comportamento de compra:

| Métrica | Descrição |
|---------|-----------|
| **R** — Recency | Dias desde a última compra |
| **F** — Frequency | Número de pedidos únicos |
| **M** — Monetary | Receita total gerada |

### 4. Segmentação — K-Means
Clusterização com transformação logarítmica + normalização + método Elbow (k=4):

| Segmento | Clientes | Recency média | Frequency média | % Receita |
|----------|----------|---------------|-----------------|-----------|
| 👑 VIP | 1.179 | 27 dias | 19 pedidos | **70,66%** |
| 🌱 Promissor | 1.237 | 29 dias | 3 pedidos | 6,96% |
| ⚠️ Em Risco | 1.432 | 227 dias | 5 pedidos | 18,12% |
| 💤 Perdido | 1.968 | 394 dias | 1 pedido | 4,26% |

### 5. Predição de Churn — Random Forest
Classificação binária com label engenheirado a partir dos segmentos:

| Modelo | Acurácia | ROC-AUC |
|--------|----------|---------|
| Regressão Logística (baseline) | 93% | 0.9846 |
| **Random Forest (final)** | **98%** | **0.9993** |

**Importância das features:**
- Recency: 73% — o principal preditor de churn
- Monetary: 13,7%
- Frequency: 13,4%

---

## 🏗️ Arquitetura do projeto

```
src/
├── preprocessing.py       # Limpeza e validação dos dados
├── feature_engineering.py # Cálculo RFM + transformação log
├── segmentation.py        # K-Means + nomeação dinâmica de clusters
├── prediction.py          # Random Forest + predição de churn
├── evaluation.py          # Relatórios e visualizações
└── pipeline.py            # Orquestração completa — um único comando
```

O pipeline é executado com:

```python
from src.pipeline import run_pipeline
rfm = run_pipeline()
```

---

## 🖥️ App de Demonstração

Interface interativa construída com Streamlit com 3 páginas:

**📊 Visão Geral** — KPIs dos segmentos, gráficos e tabela resumo

**🔍 Busca de Cliente** — Consulta por ID + simulador de novo cliente com predição em tempo real

**🎯 Estratégias** — Ações de vendas recomendadas por segmento

### Como rodar

```bash
# Instalar dependências
pip install -r requirements.txt

# Rodar o app
streamlit run app.py
```

---

## 📊 Principais insights de negócio

```
→ Top 20% dos clientes geram 70,6% da receita (Pareto confirmado)
→ Janela de maior conversão: Quinta-feira entre 10h e 14h
→ Risco de churn concentrado em Jan/Fev — melhor momento para reativar
→ EIRE: 5 clientes VIP responsáveis por volume desproporcional
→ Recency é o preditor mais forte de churn (73% de importância)
```

---

## 🛠️ Stack

| Categoria | Tecnologia |
|-----------|-----------|
| Linguagem | Python 3.10+ |
| Manipulação de dados | Pandas, NumPy |
| Machine Learning | Scikit-learn |
| Visualização | Matplotlib, Seaborn |
| App | Streamlit |
| Versionamento | Git / GitHub |

---

## 👤 Autor

**Moisés Ribeiro**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-moisesrsjr-0077B5?logo=linkedin)](https://www.linkedin.com/in/moisesrsjr/)
[![GitHub](https://img.shields.io/badge/GitHub-moises--rb-181717?logo=github)](https://github.com/moises-rb)
[![Medium](https://img.shields.io/badge/Medium-moises.rsjr-12100E?logo=medium)](https://medium.com/@moises.rsjr)

---

*Pipeline completo — do dado bruto ao app interativo.*

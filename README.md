# 🚨 Análise de Acidentes em Rodovias Federais Brasileiras (2017–2025)

![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=flat&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-2.x-150458?style=flat&logo=pandas&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=flat&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Em%20desenvolvimento-orange?style=flat)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)

> Análise exploratória completa de **609.532 registros** de acidentes em rodovias 
> federais brasileiras, unindo dados oficiais da PRF (2025) com dados históricos 
> do Kaggle (2017–2024). O projeto cobre desde a limpeza e tratamento dos dados 
> até dashboards interativos no Power BI.

---

## 📌 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Principais Insights](#-principais-insights)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Como Reproduzir](#-como-reproduzir)
- [Dashboard Power BI](#-dashboard-power-bi)
- [Nota Técnica](#️-nota-técnica--inconsistência-nos-dados-de-2025)
- [Próximas Etapas](#-próximas-etapas)
- [Autor](#-autor)

---

## 📋 Sobre o Projeto

Este projeto analisa **609.532 acidentes** registrados em rodovias federais 
brasileiras entre 2017 e 2025, a partir da união de dois datasets:

| Dataset | Fonte | Período | Registros | Granularidade |
|---|---|---|---|---|
| Acidentes PRF | [PRF Dados Abertos](https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos) | 2025 | ~584k linhas | Por pessoa |
| Acidentes Históricos | [Kaggle](https://www.kaggle.com/) | 2017–2024 | ~547k linhas | Por acidente |

O pipeline completo inclui:
- Limpeza e tratamento de dados sujos com valores ausentes e inconsistências
- Padronização de categorias entre os dois datasets
- Resolução de diferença de granularidade (pessoa vs. acidente)
- Análise exploratória visual com 5 gráficos principais
- Dashboard interativo com 5 páginas no Power BI

---

## 🔍 Principais Insights

| # | Insight | Dado |
|---|---|---|
| 1 | A maioria dos acidentes ocorre com **céu claro** | 370k de 609k registros |
| 2 | **Pleno dia** é mais perigoso que a noite inteira | 337k vs 210k acidentes |
| 3 | **MG, SC e PR** concentram 36% de todos os acidentes | Top 3 estados |
| 4 | **Reação tardia do condutor** é a causa mais frequente | ~150k acidentes |
| 5 | **Outubro** é o mês mais perigoso do ano | ~54k acidentes |

---

## 📁 Estrutura do Projetoacidentes-rodovias-federais-br/
│
├── Dados/                                    # Dados (não versionados — ver nota)
│   ├── raw/                                  # Datasets originais
│   └── processed/                            # Dataset tratado gerado pelo notebook
│
├── notebooks_Lucas.Boros/                    # Notebooks Jupyter
│   ├── 1-EDA_Limpeza.ipynb                  # ✅ EDA, limpeza e tratamento
│   ├── 2-Feature_Engineering.ipynb          # 🔄 Em desenvolvimento
│   ├── 3-Modelo_ML.ipynb                    # 🔄 Em desenvolvimento
│   ├── graficos/                             # Gráficos gerados pelo notebook 1
│   └── requirements.txt                      # Dependências do projeto
│
├── dashboard-PowerBI_Lucas.Boros/            # Dashboard Power BI
│   ├── acidentes_rodoviasBR.pbix            # Arquivo do dashboard
│   ├── Imagens/                              # Imagens utilizadas no dashboard
│   └── icones/                               # Ícones utilizados no dashboard
│
├── .gitignore
├── LICENSE
└── README.md

---

## 🛠️ Tecnologias Utilizadas

| Categoria | Tecnologia |
|---|---|
| Linguagem | Python 3.13 |
| Manipulação de dados | pandas, numpy |
| Visualização | matplotlib, seaborn, missingno |
| Ambiente | Jupyter Notebook, VS Code, conda |
| Dashboard | Power BI Desktop |
| Versionamento | Git, GitHub |

---

## 🚀 Como Reproduzir

### Pré-requisitos
- [Anaconda](https://www.anaconda.com/) ou Miniconda instalado
- [VS Code](https://code.visualstudio.com/) com extensão Jupyter
- [Power BI Desktop](https://powerbi.microsoft.com/) para visualizar o dashboard

### 1. Clone o repositório
```bashgit clone https://github.com/Lucas-Coutinhob/acidentes-rodovias-federais-br.git
cd acidentes-rodovias-federais-br

### 2. Crie o ambiente virtual
```bashconda create -n acidentes-br python=3.13
conda activate acidentes-br
pip install -r notebooks_Lucas.Boros/requirements.txt

### 3. Baixe os dados brutos
Os dados não estão versionados por excederem o limite de 100MB do GitHub.
Faça o download manualmente:

- **PRF 2025:** [gov.br/prf — Dados Abertos](https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos)
- **2017–2024:** [Kaggle — Acidentes em Rodovias Federais](https://www.kaggle.com/)

Coloque os arquivos baixados em `Dados/raw/`

### 4. Execute o notebook
Abra `notebooks_Lucas.Boros/1-EDA_Limpeza.ipynb` no VS Code,  
selecione o kernel `Python (acidentes-br)` e execute todas as células.

O dataset tratado será gerado automaticamente em `Dados/processed/`.

---

## 📊 Dashboard Power BI

O dashboard contém **5 páginas** com análises interativas:

| Página | Conteúdo |
|---|---|
| 🏠 Capa | Navegação e apresentação do projeto |
| 📊 Visão Geral | KPIs principais, evolução anual e distribuição geográfica |
| 🕐 Análise Temporal | Heatmap dia×hora, acidentes por mês e fase do dia |
| ⚠️ Causas e Tipos | Top causas, tipos mais fatais e condição meteorológica |
| 🗺️ Análise Geográfica | Mapa por estado, top rodovias e municípios |

> O arquivo `.pbix` está disponível em `dashboard-PowerBI_Lucas.Boros/`.  
> Requer **Power BI Desktop** para visualização e interação.

---

## ⚠️ Nota Técnica — Inconsistência nos Dados de 2025

Durante a análise, identificou-se que o dataset da PRF de 2025 possui 
**granularidade por pessoa** (cada linha = uma pessoa envolvida), enquanto 
o dataset histórico 2017–2024 possui **granularidade por acidente** 
(cada linha = um acidente).

A solução adotada foi agregar o dataset 2025 usando `groupby('id')`, 
aplicando `sum` nas colunas de vítimas. Posteriormente, identificou-se 
que o uso de `sum` gerava **duplicação artificial** dos valores de mortos, 
pois o campo já representava o total do acidente em cada linha.

**Correção aplicada:** substituição de `sum` por `max` na agregação das 
colunas de vítimas — capturando o valor real sem duplicação.

Esta decisão está documentada com justificativa completa no notebook `1-EDA_Limpeza.ipynb`.

---

## 🗺️ Próximas Etapas

- [x] Notebook 1 — EDA, limpeza e tratamento dos dados
- [x] Dashboard Power BI com 5 páginas analíticas
- [ ] Notebook 2 — Feature Engineering e preparação para ML
- [ ] Notebook 3 — Modelo de Machine Learning para predição de acidentes fatais
- [ ] Publicação do modelo com métricas de avaliação

---

## 👤 Autor

**Lucas Coutinho Boros**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Lucas%20Coutinho%20Boros-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/lucas-coutinho-boros)
[![GitHub](https://img.shields.io/badge/GitHub-Lucas--Coutinhob-181717?style=flat&logo=github&logoColor=white)](https://github.com/Lucas-Coutinhob)

---

*Dados: PRF Dados Abertos + Kaggle | Período: janeiro/2017 a março/2025*

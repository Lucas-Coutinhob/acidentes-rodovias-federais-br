# 📓 Notebooks — Análise de Acidentes em Rodovias Federais

Este diretório contém os notebooks Jupyter desenvolvidos ao longo do projeto,
organizados em etapas sequenciais do pipeline de ciência de dados.

---

## 📋 Índice dos Notebooks

| # | Notebook | Status | Descrição |
|---|---|---|---|
| 1 | `1-EDA_Limpeza.ipynb` | ✅ Concluído | EDA, limpeza, tratamento e merge dos datasets |
| 2 | `2-Feature_Engineering.ipynb` | 🔄 Em desenvolvimento | Engenharia de atributos e encoding para ML |
| 3 | `3-Modelo_ML.ipynb` | 🔄 Em desenvolvimento | Modelo preditivo de acidentes fatais |

---

## 📔 Notebook 1 — EDA, Limpeza e Tratamento

**Arquivo:** `1-EDA_Limpeza.ipynb`

### O que foi feito

#### Etapa 1 — Seleção de colunas comuns
Dos dois datasets com estruturas diferentes, foram mantidas apenas as 
**26 colunas presentes em ambos**, descartando colunas exclusivas de cada fonte.

#### Etapa 2 — Conversão de tipos
| Coluna | Tipo Original | Tipo Final |
|---|---|---|
| `data_inversa` | string | datetime64 |
| `latitude` / `longitude` | string (vírgula) | float64 |
| `km` | string (vírgula) | float64 |
| `br`, `mortos`, `feridos_*`, `ilesos` | float64 | Int64 (nullable) |

#### Etapa 3 — Tratamento de valores ausentes
Estratégia mista baseada na natureza de cada coluna:
- **Remoção** de linhas com NaN em colunas estruturais (< 0,08% dos dados)
- **`fillna(0)`** nas colunas de vítimas do dataset 2025 — NaN estrutural 
  confirmado por investigação (granularidade por pessoa)

#### Etapa 4 — Padronização de categorias
Inconsistências identificadas e tratadas em `causa_acidente` e `sentido_via`:
- **Tipo 1:** duplicatas por capitalização inconsistente
- **Tipo 2:** categorias renomeadas entre as versões do sistema PRF
- **Tipo 3:** categorias exclusivas do período histórico — mantidas

#### Etapa 5 — Tratamento de duplicatas
O dataset 2025 possuía **granularidade por pessoa** (média de 8,1 linhas 
por acidente). Solução: agregação com `groupby('id')` usando `max` nas 
colunas de vítimas e `first` nas demais.

#### Etapa 6 — Merge final
União dos dois datasets com `pd.concat()` após adição da coluna `fonte` 
para rastreabilidade da origem de cada registro.

### Resultado final
| Métrica | Valor |
|---|---|
| Total de registros | 609.532 |
| Total de colunas | 27 |
| Valores ausentes | 0 |
| Duplicatas | 0 |
| Período coberto | jan/2017 a mar/2025 |

### Gráficos gerados
Os gráficos estão salvos na pasta `graficos/`:

| Arquivo | Gráfico |
|---|---|
| `01_evolucao_anual.png` | Evolução anual do número de acidentes |
| `02_top10_causas.png` | Top 10 causas de acidentes |
| `03_fase_dia_classificacao.png` | Acidentes por fase do dia e classificação |
| `04_top15_estados.png` | Top 15 estados com mais acidentes |
| `05_mortos_por_ano.png` | Mortos por ano — total e média por acidente |

---

## 📔 Notebook 2 — Feature Engineering *(em desenvolvimento)*

**Arquivo:** `2-Feature_Engineering.ipynb`

Próximas etapas planejadas:
- Criação da variável alvo `acidente_fatal` (binária: 0/1)
- Extração de features temporais (`ano`, `mes`, `hora`, `periodo_dia`)
- Ordinal Encoding nas variáveis com ordem natural
- One-Hot Encoding nas variáveis nominais
- Normalização das variáveis numéricas
- Exportação do dataset final para o notebook de ML

---

## 📔 Notebook 3 — Modelo de Machine Learning *(em desenvolvimento)*

**Arquivo:** `3-Modelo_ML.ipynb`

Próximas etapas planejadas:
- Variável alvo: `acidente_fatal`
- Split treino/teste estratificado
- Treinamento e comparação de modelos
- Métricas de avaliação (precisão, recall, F1, AUC-ROC)
- Interpretação com SHAP values

---

## ⚙️ Ambiente de Desenvolvimento

```bash
# Criar o ambiente
conda create -n acidentes-br python=3.13
conda activate acidentes-br

# Instalar dependências
pip install -r requirements.txt

# Registrar o kernel no Jupyter
python -m ipykernel install --user --name acidentes-br --display-name "Python (acidentes-br)"
```

---

*Para instruções completas de reprodução, consulte o [README principal](../README.md)*

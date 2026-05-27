# Rede Neural para Identificação de Tensões e Sensibilidades Sociopolíticas Regionais

Estudo aplicado de *deep representation learning* sobre dados agregados do **Censo Demográfico 2022 (IBGE)**. Um *autoencoder* simétrico com gargalo bidimensional comprime cerca de 5.570 municípios brasileiros em um plano latente que é, em seguida, clusterizado e interpretado como conjunto de **perfis estruturais latentes**.

> O trabalho é **descritivo e exploratório**. Não há previsão eleitoral, modelagem causal nem inferência política agressiva.

## Estrutura

| Arquivo | Descrição |
|---|---|
| `Rede_Neural_Censo_2022.ipynb` | Notebook principal, mini-paper completo |
| `bases/` | (não versionada) CSVs brutos do Censo 2022 |

## Como executar

1. Baixar os agregados por município do Censo 2022 em <https://www.ibge.gov.br/estatisticas/downloads-estatisticas.html> e colocar os `.zip` na raiz do projeto **ou** os `.csv` extraídos em `./bases/`.
2. Criar ambiente Python 3.10+ e instalar:
   ```bash
   pip install numpy pandas matplotlib seaborn plotly scikit-learn tensorflow umap-learn nbformat
   ```
3. Abrir `Rede_Neural_Censo_2022.ipynb` no Jupyter ou no VS Code e executar.

## Pipeline

```
CSVs Censo 2022
      │
      ▼
limpeza + engenharia leve
      │
      ▼
StandardScaler
      │
      ▼
Autoencoder (64 → 32 → 2 → 32 → 64)
      │
      ▼
embeddings latentes 2D
      │
      ▼
KMeans + silhouette
      │
      ▼
interpretação dos perfis
```

## Dados

Quatro temas, todos baixados do portal IBGE:

- `agregados_por_municipios_basico_BR.csv`
- `agregados_por_municipios_alfabetizacao_BR.csv`
- `agregados_por_municipios_caracteristicas_domicilio1_BR.csv`
- `agregados_por_municipios_demografia_BR.csv`

Os CSVs **não são versionados** (`.gitignore`). A leitura é tolerante a separador (`;` ou `,`) e encoding (`latin-1` ou `utf-8`).

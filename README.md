# Rede Neural para Caracterização de Perfis Regionais de Alfabetização

Trabalho de **Deep Learning** (graduação em Ciência de Dados). Usamos uma **rede neural densa (MLP)** sobre os dados do **Censo Demográfico 2022 (IBGE)** para **prever a taxa de alfabetização de adultos** de cada município brasileiro a partir de características estruturais (região, porte, urbanização e estrutura etária) — e para descobrir **quais desses fatores mais explicam** a alfabetização.

> Trabalho **descritivo e exploratório**. Não faz previsão eleitoral nem inferência causal/política.

## Pergunta de pesquisa

> Quais características estruturais de um município explicam a sua taxa de alfabetização — e uma rede neural prevê melhor do que um modelo linear simples?

## Dados

Censo Demográfico 2022 (IBGE), agregados por município (5.570 municípios), na pasta [`bases/`](bases/):

| Arquivo | Conteúdo |
|---|---|
| `Agregados_por_municipios_basico_BR.csv` | região, UF, área e população |
| `Agregados_por_municipios_alfabetizacao_BR.csv` | população de 15+ anos (total e alfabetizada), por faixa etária |

**Alvo:** taxa de alfabetização = `alfabetizados 15+ ÷ população 15+`. A taxa nacional calculada (**93,2%**) bate com a oficial do IBGE (~93%), validando a construção da variável.

## Modelo

- **MLP (`MLPRegressor` do scikit-learn)** — rede densa com camadas `(64, 32)` e ativação ReLU.
- Pré-processamento: padronização (z-score) e divisão treino/teste 80/20.
- Cuidados: regularização L2 (`alpha`) e *early stopping* contra *overfitting*.
- Comparada contra *baselines* (média, média por região, regressão linear).

## Resultados

| Modelo | R² (teste) |
|---|---|
| Média (baseline) | ~0,00 |
| Média por região | ~0,69 |
| Regressão Linear | ~0,76 |
| **Rede Neural (MLP)** | **~0,80** |

Os fatores que mais explicam a alfabetização são a **região** e a **estrutura etária** da população.

## Estrutura do repositório

| Arquivo | Descrição |
|---|---|
| [`Rede_Neural_Final.ipynb`](Rede_Neural_Final.ipynb) | notebook principal, comentado e executado |
| [`Apresentacao_Rede_Neural.pptx`](Apresentacao_Rede_Neural.pptx) | apresentação do trabalho |
| [`bases/`](bases/) | dados do Censo 2022 (IBGE) |

## Como executar

```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```

Abra o `Rede_Neural_Final.ipynb` no Jupyter ou no VS Code e execute as células de cima para baixo. A primeira célula já instala as dependências automaticamente (útil no Google Colab).

## Equipe

Cesar Fonseca · Matheus Lima · Vinicius de Paula

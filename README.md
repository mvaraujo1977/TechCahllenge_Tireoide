# Tech Challenge - Classificação de Hipotireoidismo

Projeto desenvolvido para a Fase 1 do curso de Pós-Graduação em IA para Devs, com foco em Machine Learning supervisionado aplicado a dados médicos tabulares.

## Objetivo

O objetivo do projeto é construir uma solução inicial de apoio à análise clínica para classificar registros relacionados à tireoide entre as classes `hypothyroid` e `negative`.

A solução utiliza dados estruturados, técnicas de análise exploratória, pipelines de pré-processamento e modelos de classificação. O modelo deve ser entendido como apoio à triagem e à priorização de análise, sem substituir avaliação médica.

## Dataset

O dataset utilizado está disponível na pasta `dataset/`:

- `hypothyroid.data`: arquivo original com os registros.
- `hypothyroid.names`: identificação das colunas.
- `hypothyroid_final.csv`: base consolidada usada no notebook.

No Google Colab, o notebook baixa automaticamente o arquivo `hypothyroid_final.csv` diretamente do GitHub.

## Estrutura do Projeto

```text
.
├── dataset/
│   ├── hypothyroid.data
│   ├── hypothyroid.names
│   └── hypothyroid_final.csv
├── models/
│   └── modelo_classificacao_tireoide.pkl
├── notebooks/
│   └── 01_classificacao_tireoide.ipynb
├── reports/
│   └── figures/
├── Dockerfile
├── README.md
└── requirements.txt
```

## Execução no Google Colab

1. Abra o notebook `notebooks/01_classificacao_tireoide.ipynb` no Google Colab.
2. Execute a célula opcional de instalação de dependências, se necessário.
3. Execute as células em ordem.
4. O dataset será baixado automaticamente do GitHub para `/content/TechCahllenge_Tireoide/dataset/`.
5. O modelo treinado será salvo em `models/modelo_classificacao_tireoide.pkl`.

## Execução Local

Crie um ambiente virtual e instale as dependências:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

No Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
jupyter notebook
```

## Modelos Avaliados

Foram avaliados três modelos de classificação:

- Regressão Logística.
- Random Forest Classifier.
- HistGradientBoostingClassifier com early stopping.

O pipeline utiliza imputação de valores ausentes, padronização de variáveis numéricas quando necessário, codificação one-hot para variáveis categóricas e `ColumnTransformer` para evitar data leakage.

## Resultado Final

O melhor modelo selecionado foi o **Random Forest**. No conjunto de teste, os resultados obtidos foram:

| Métrica | Valor |
| --- | ---: |
| Accuracy | 0.991 |
| Precision | 0.905 |
| Recall | 0.905 |
| F1-score | 0.905 |
| AUC | 0.996 |

As variáveis com maior influência por importância de permutação foram:

- FTI
- TSH
- TT4
- age
- on_thyroxine

## Observações Éticas

O modelo desenvolvido tem finalidade acadêmica e exploratória. Ele pode apoiar triagem ou análise inicial, mas não substitui avaliação médica.

A decisão final sobre diagnóstico e conduta deve permanecer sempre sob responsabilidade de profissionais da saúde, considerando histórico clínico, exame físico, protocolos institucionais e exames complementares.

## Docker

O Dockerfile fornece um ambiente básico para execução do notebook.

```bash
docker build -t techchallenge-tireoide .
docker run -p 8888:8888 techchallenge-tireoide
```

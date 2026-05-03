# Tech Challenge - IA Aplicada à Saúde

Projeto desenvolvido para a Fase 1 da Pós-Graduação em IA para Devs, com foco em uma solução inicial de apoio à análise de dados médicos. A entrega principal utiliza Machine Learning supervisionado em dados tabulares para classificação de registros relacionados à tireoide. Como complemento, foi desenvolvida uma etapa extra de Visão Computacional aplicada a imagens de ressonância magnética cerebral.

O projeto tem finalidade acadêmica e exploratória. Os modelos construídos devem ser interpretados como ferramentas de apoio à triagem e à análise inicial, nunca como substitutos da avaliação médica.

## Visão Geral

O desafio proposto considera o contexto de um hospital universitário que busca soluções inteligentes para apoiar a análise inicial de exames e dados clínicos. Nesta primeira fase, a prioridade é construir uma base de sistema de IA com modelos de classificação, explorando dados estruturados e, de forma extra, imagens médicas.

A solução está organizada em duas frentes:

- **Parte principal:** classificação tabular de registros relacionados à tireoide, com o objetivo de identificar casos `hypothyroid` ou `negative`.
- **Parte extra:** classificação de imagens de MRI cerebral, comparando uma CNN simples com um modelo baseado em Transfer Learning.

Em ambas as frentes, o foco está em boas práticas de ciência de dados: análise exploratória, pré-processamento adequado, separação entre treino/validação/teste, avaliação por métricas relevantes, interpretação dos resultados e discussão das limitações.

## Objetivos

Os objetivos principais do projeto são:

- organizar e documentar uma base médica tabular;
- construir pipelines de pré-processamento para evitar vazamento de dados;
- treinar e comparar modelos supervisionados de classificação;
- avaliar os resultados com métricas adequadas ao contexto médico;
- interpretar o comportamento dos modelos;
- discutir riscos, limitações e possibilidades de uso;
- complementar a solução com um experimento de Visão Computacional em imagens médicas.

## Estrutura do Repositório

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
├── extra/
│   ├── 02_visao_computacional_mri_cancer.ipynb
│   ├── README.md
│   └── models/
│       ├── best_image_classifier.keras
│       ├── cnn_simples.keras
│       └── transfer_learning_model.keras
├── model_tireoide.ipynb
├── Dockerfile
├── README.md
└── requirements.txt
```

## Acessos Diretos

- Notebook principal: [01_classificacao_tireoide.ipynb](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/notebooks/01_classificacao_tireoide.ipynb)
- Notebook auxiliar de preparação dos dados tabulares: [model_tireoide.ipynb](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/model_tireoide.ipynb)
- Notebook extra de Visão Computacional: [02_visao_computacional_mri_cancer.ipynb](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/extra/02_visao_computacional_mri_cancer.ipynb)
- README da parte extra: [extra/README.md](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/extra/README.md)
- Dockerfile: [Dockerfile](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/Dockerfile)
- Dependências: [requirements.txt](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/requirements.txt)
- Dataset consolidado tabular: [hypothyroid_final.csv](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/dataset/hypothyroid_final.csv)
- Modelo tabular salvo: [modelo_classificacao_tireoide.pkl](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/models/modelo_classificacao_tireoide.pkl)
- Melhor modelo de imagem salvo: [best_image_classifier.keras](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/extra/models/best_image_classifier.keras)

## Dataset Tabular

O dataset principal foi retirado do **UCI Machine Learning Repository**, no conjunto **Thyroid Disease**:

[Thyroid Disease - UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/102/thyroid+disease)

No repositório original, os dados são disponibilizados em arquivos separados. Para este projeto, foram utilizados:

- `hypothyroid.data`: arquivo original com os registros;
- `hypothyroid.names`: descrição dos atributos;
- `hypothyroid_final.csv`: versão consolidada usada na modelagem.

O arquivo `model_tireoide.ipynb`, localizado na raiz do repositório, foi usado apenas como etapa inicial de apoio para organizar os arquivos originais e gerar a base consolidada `hypothyroid_final.csv`. A análise final, os modelos, as avaliações e o relatório técnico da parte principal estão no notebook:

[notebooks/01_classificacao_tireoide.ipynb](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/notebooks/01_classificacao_tireoide.ipynb)

## Parte Principal - Classificação de Hipotireoidismo

A tarefa principal foi formulada como um problema de classificação supervisionada com dados tabulares. O objetivo é classificar registros entre:

- `hypothyroid`;
- `negative`.

O notebook principal contempla:

- carregamento do dataset;
- inspeção de dimensões, tipos e estatísticas descritivas;
- análise de valores ausentes;
- análise de duplicados;
- distribuição da variável-alvo;
- análise de balanceamento das classes;
- visualizações exploratórias;
- análise de correlação;
- limpeza dos dados;
- separação entre variáveis preditoras e variável-alvo;
- divisão entre treino, validação e teste;
- pipeline de pré-processamento com `ColumnTransformer`;
- imputação de valores ausentes;
- padronização de variáveis numéricas quando necessário;
- codificação one-hot para variáveis categóricas;
- comparação entre modelos;
- análise de métricas e matriz de confusão;
- interpretação por importância de variáveis;
- relatório final e discussão crítica.

### Modelos Avaliados

Foram avaliadas três abordagens:

- Regressão Logística;
- Random Forest Classifier;
- HistGradientBoostingClassifier com early stopping.

A escolha dos modelos considerou diversidade de técnicas, interpretabilidade e desempenho em um problema de classificação médica. O uso de pipelines do `scikit-learn` reduz o risco de data leakage, pois as transformações são ajustadas somente nos dados de treino dentro de cada etapa de modelagem.

### Resultado da Parte Principal

O melhor modelo selecionado foi o **Random Forest**. No conjunto de teste, foram obtidos os seguintes resultados:

| Métrica | Valor |
| --- | ---: |
| Accuracy | 0.991 |
| Precision | 0.905 |
| Recall | 0.905 |
| F1-score | 0.905 |
| AUC | 0.996 |

As variáveis com maior influência por importância de permutação foram:

- `FTI`;
- `TSH`;
- `TT4`;
- `age`;
- `on_thyroxine`.

Esses resultados indicam bom desempenho experimental, mas não devem ser interpretados como validação clínica. A base utilizada, a forma de coleta e o contexto de aplicação precisam ser considerados antes de qualquer uso prático.

## Parte Extra - Visão Computacional

A pasta `extra/` contém a etapa complementar com imagens de ressonância magnética cerebral:

```text
extra/
├── 02_visao_computacional_mri_cancer.ipynb
├── README.md
└── models/
```

Essa etapa utiliza o dataset público **Brain Cancer MRI Dataset**, baixado diretamente do Kaggle com `kagglehub`. O notebook inspeciona a estrutura real dos arquivos antes de assumir classes ou formatos, realiza análise exploratória das imagens, treina uma CNN simples e compara o desempenho com um modelo MobileNetV2 usando Transfer Learning e fine-tuning.

A interpretação visual é feita com Grad-CAM. Essa técnica destaca regiões que influenciaram a predição do modelo, mas não representa segmentação médica validada. Como o dataset não possui bounding boxes nem máscaras, não foi implementado treinamento YOLO para detecção ou segmentação.

Os detalhes da parte extra estão documentados em:

[extra/README.md](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/extra/README.md)

### Observação Sobre os Modelos da Parte Extra

Quando o notebook extra é executado no Google Colab, os modelos `.keras` são salvos na pasta `models/` do ambiente de execução. No repositório, para manter a organização da entrega, os modelos treinados foram armazenados em:

```text
extra/models/
```

## Execução no Google Colab

A execução recomendada é pelo Google Colab, especialmente para a parte de Visão Computacional.

### Parte Tabular

1. Abra [notebooks/01_classificacao_tireoide.ipynb](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/notebooks/01_classificacao_tireoide.ipynb) no Google Colab.
2. Execute a célula opcional de instalação de dependências, se necessário.
3. Execute as células em ordem.
4. O dataset tabular será baixado automaticamente do GitHub para o ambiente do Colab.
5. O modelo final será salvo em `models/modelo_classificacao_tireoide.pkl`.

### Parte Extra

1. Abra [extra/02_visao_computacional_mri_cancer.ipynb](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/extra/02_visao_computacional_mri_cancer.ipynb) no Google Colab.
2. Verifique se a GPU está habilitada.
3. Execute a célula de instalação de dependências, se necessário.
4. Execute o download do dataset com `kagglehub`.
5. Execute as células em ordem.
6. Ao final, confira os modelos salvos e as visualizações Grad-CAM.

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

Depois, abra os notebooks pela interface do Jupyter.

## Execução com Docker

O `Dockerfile` fornece um ambiente básico para execução dos notebooks.

```bash
docker build -t techchallenge-tireoide .
docker run -p 8888:8888 techchallenge-tireoide
```

Após iniciar o container, acesse o endereço informado no terminal do Jupyter.

## Dependências

As principais bibliotecas utilizadas são:

- `pandas`;
- `numpy`;
- `matplotlib`;
- `seaborn`;
- `scikit-learn`;
- `joblib`;
- `shap`;
- `tensorflow`;
- `opencv-python`;
- `Pillow`;
- `kagglehub`;
- `tqdm`;
- `jupyter`.

As dependências completas estão em:

[requirements.txt](https://github.com/mvaraujo1977/TechCahllenge_Tireoide/blob/Nirton_Afonso/requirements.txt)

## Artefatos Gerados

Os principais modelos salvos no repositório são:

```text
models/
└── modelo_classificacao_tireoide.pkl

extra/models/
├── best_image_classifier.keras
├── cnn_simples.keras
└── transfer_learning_model.keras
```

O arquivo `modelo_classificacao_tireoide.pkl` corresponde ao melhor pipeline da etapa tabular. Na parte extra, `best_image_classifier.keras` representa o melhor modelo de classificação de imagens.

## Limitações

Este projeto deve ser interpretado como uma prova de conceito acadêmica. Entre as principais limitações, destacam-se:

- uso de bases públicas específicas;
- ausência de validação externa;
- ausência de validação prospectiva em ambiente clínico;
- possibilidade de vieses relacionados à origem dos dados;
- dependência de qualidade e representatividade das bases utilizadas;
- possibilidade de variação nos resultados conforme ambiente, GPU e versões de bibliotecas;
- ausência de máscaras ou bounding boxes na parte de imagens;
- necessidade de revisão especializada para qualquer uso real.

No caso da parte tabular, a importância das variáveis não implica causalidade. No caso da parte de imagens, Grad-CAM não deve ser interpretado como segmentação anatômica precisa.

## Considerações Éticas

Modelos de IA em saúde devem ser utilizados com cautela. Mesmo quando apresentam bons resultados quantitativos, eles podem errar, reproduzir vieses ou falhar em populações e cenários diferentes daqueles observados no treinamento.

O objetivo deste projeto é apoiar a análise inicial e a triagem, não substituir profissionais da saúde. A decisão final sobre diagnóstico, investigação complementar e conduta clínica deve permanecer sempre com médicos e equipes qualificadas, considerando histórico, exame físico, protocolos institucionais e exames complementares.

## Possíveis Melhorias

Como continuidade do projeto, recomenda-se:

- validar os modelos em bases externas;
- avaliar calibração de probabilidades;
- investigar ajuste de limiar de decisão;
- ampliar a análise de vieses;
- revisar os resultados com especialistas da área médica;
- documentar cenários de uso e não uso;
- criar um conjunto anotado por especialistas para detecção ou segmentação na parte de imagens;
- melhorar a rastreabilidade dos experimentos;
- criar um relatório PDF final consolidado com gráficos, resultados e link do repositório.

## Entregáveis Relacionados ao Tech Challenge

Este repositório contém:

- código-fonte completo;
- notebooks com execução e resultados;
- dataset tabular consolidado;
- link e download automatizado do dataset de imagens;
- modelos treinados;
- README com instruções de execução;
- Dockerfile;
- relatórios finais dentro dos notebooks.

Além do repositório, o Tech Challenge solicita a entrega de um PDF final com o link do Git, resultados, prints/gráficos e relatório técnico, além de um vídeo demonstrativo de até 15 minutos.

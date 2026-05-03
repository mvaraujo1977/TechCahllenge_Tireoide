# Parte Extra - Visão Computacional em MRI Cerebral

Este diretório reúne a etapa extra do Tech Challenge, dedicada ao uso de Visão Computacional em imagens de ressonância magnética cerebral. A proposta complementa a etapa principal do projeto, baseada em dados tabulares, explorando agora um fluxo de classificação de imagens médicas.

O trabalho tem finalidade acadêmica e foi desenvolvido como uma prova de conceito. O modelo não deve ser entendido como ferramenta diagnóstica independente, mas como uma solução experimental que pode apoiar uma triagem inicial ou uma análise preliminar sob supervisão profissional.

## Objetivo

O objetivo desta etapa é construir e avaliar modelos de classificação para imagens de MRI cerebral, comparando uma rede neural convolucional treinada do zero com uma abordagem de Transfer Learning.

O notebook cobre as seguintes etapas:

- download do dataset com `kagglehub`;
- inspeção automática da estrutura real dos arquivos;
- identificação de classes a partir das pastas;
- verificação de extensões, dimensões, canais e imagens corrompidas;
- análise exploratória visual e estatística das imagens;
- avaliação de brilho, contraste, balanceamento e duplicatas;
- preparação dos dados com redimensionamento, normalização e divisão estratificada;
- uso de `data augmentation` apenas no conjunto de treino;
- treinamento de uma CNN simples;
- treinamento de um modelo MobileNetV2 com Transfer Learning e fine-tuning;
- avaliação com accuracy, precision, recall, F1-score, matriz de confusão e AUC macro;
- interpretação visual com Grad-CAM;
- salvamento dos modelos treinados;
- discussão final sobre limitações, riscos e melhorias futuras.

## Estrutura

```text
extra/
├── 02_visao_computacional_mri_cancer.ipynb
├── README.md
├── data/
├── models/
│   ├── best_image_classifier.keras
│   ├── cnn_simples.keras
│   └── transfer_learning_model.keras
└── reports/
```

A pasta `data/` é gerada durante a execução e não precisa ser versionada. Os modelos salvos em `extra/models/` representam os artefatos treinados nesta etapa.

## Dataset

O dataset utilizado é o **Brain Cancer MRI Dataset**, disponível no Kaggle:

[Brain Cancer MRI Dataset - Kaggle](https://www.kaggle.com/datasets/orvile/brain-cancer-mri-dataset)

O download é realizado diretamente no notebook com:

```python
import kagglehub

path = kagglehub.dataset_download("orvile/brain-cancer-mri-dataset")
```

Após o download, os arquivos são organizados em:

```text
data/raw/brain_cancer_mri/
```

Na execução registrada no notebook, a inspeção identificou 6.057 arquivos, sendo 6.056 imagens `.jpg` e um arquivo `.csv`. As classes foram inferidas pela estrutura de pastas:

| Classe | Quantidade |
| --- | ---: |
| `brain_glioma` | 2.004 |
| `brain_menin` | 2.004 |
| `brain_tumor` | 2.048 |

Todas as imagens inspecionadas estavam válidas, em modo RGB, com dimensão original predominante de 512x512 pixels.

## Análise Exploratória

A análise exploratória indicou que a base é relativamente balanceada entre as três classes, o que favorece a avaliação por métricas macro. Também foram identificadas 44 possíveis duplicatas por hash, concentradas nos registros exibidos na inspeção.

Esse ponto é relevante porque duplicatas podem levar a estimativas otimistas de desempenho se imagens equivalentes aparecerem em subconjuntos diferentes. Em uma continuidade do projeto, a remoção ou o controle dessas duplicatas deve ser tratado antes de uma validação mais rigorosa.

Também foram observadas diferenças globais de brilho e contraste entre as classes. A classe `brain_tumor` apresentou maior intensidade média, `brain_menin` apresentou maior contraste médio e `brain_glioma` teve menor brilho médio. Essas diferenças ajudam a compreender o comportamento dos modelos, mas exigem cautela, pois podem refletir características de aquisição, origem dos dados ou pré-processamento, e não necessariamente apenas padrões anatômicos.

## Preparação dos Dados

As imagens foram redimensionadas para 224x224 pixels e normalizadas para o intervalo `[0, 1]`. A divisão dos dados foi feita de forma estratificada:

| Conjunto | Quantidade | Percentual |
| --- | ---: | ---: |
| Treino | 4.239 | 70,00% |
| Validação | 908 | 14,99% |
| Teste | 909 | 15,01% |

O `data augmentation` foi aplicado somente ao conjunto de treino. Essa decisão reduz o risco de vazamento de informação e preserva validação e teste como conjuntos mais próximos de dados não vistos.

## Modelos Treinados

Foram avaliadas duas abordagens:

**CNN simples:** modelo convolucional treinado do zero, usado como baseline para verificar se a base possui sinal visual suficiente para classificação.

**MobileNetV2 com Transfer Learning:** modelo pré-treinado em ImageNet, com treinamento inicial da cabeça classificadora e fine-tuning parcial das últimas camadas.

## Resultados

Os resultados finais no conjunto de teste foram:

| Modelo | Accuracy | Precision | Recall | F1-score | AUC |
| --- | ---: | ---: | ---: | ---: | ---: |
| CNN simples | 0,825 | 0,860 | 0,824 | 0,818 | 0,985 |
| Transfer Learning MobileNetV2 | 0,958 | 0,961 | 0,958 | 0,958 | 0,996 |

O melhor desempenho foi obtido pelo modelo **Transfer Learning MobileNetV2**. Ele apresentou melhor equilíbrio geral entre as classes e superou a CNN simples em todas as métricas avaliadas.

Na análise por classe, a CNN simples teve dificuldade relevante em `brain_menin`, com recall de 0,58. O modelo MobileNetV2 também manteve `brain_menin` como a classe mais desafiadora, mas com desempenho superior, alcançando recall de 0,90. Para `brain_tumor`, o MobileNetV2 obteve recall de 1,00 no conjunto de teste.

Em contexto de saúde, o recall merece atenção especial, pois falsos negativos podem deixar de sinalizar imagens potencialmente suspeitas. Ainda assim, falsos positivos também precisam ser considerados, pois podem gerar ansiedade, exames adicionais e sobrecarga clínica.

## Grad-CAM

A interpretação visual foi feita com Grad-CAM. A técnica gera mapas de ativação que indicam regiões da imagem que influenciaram a predição do modelo.

É importante destacar que Grad-CAM não é segmentação médica. O heatmap não delimita tumores com precisão clínica, não substitui máscaras anotadas e não deve ser usado isoladamente para apoiar diagnóstico ou conduta. Sua utilidade, neste projeto, é oferecer uma leitura exploratória sobre o comportamento do modelo.

## Detecção e Segmentação

O dataset utilizado está organizado como classificação por pastas e não apresenta anotações supervisionadas de bounding boxes ou máscaras. Por esse motivo, o notebook não implementa treinamento YOLO para detecção ou segmentação.

Essa decisão evita fabricar labels e evita sugerir uma capacidade de localização anatômica que a base não permite validar. Para uma etapa futura de detecção ou segmentação real, seria necessário construir uma base anotada por especialistas, com caixas delimitadoras ou máscaras revisadas por profissionais da área médica.

## Execução no Google Colab

Para executar o notebook no Google Colab:

1. Abra `extra/02_visao_computacional_mri_cancer.ipynb`.
2. Se necessário, execute a célula de instalação de dependências.
3. Execute a célula de download com `kagglehub`.
4. Execute as células em ordem.
5. Verifique se a GPU está disponível antes do treinamento.
6. Ao final, confira os modelos salvos em `models/`.

O notebook foi preparado para inspecionar a estrutura do dataset antes de assumir classes ou formatos. Essa verificação é importante porque bases públicas podem mudar de organização ao longo do tempo.

## Artefatos Gerados

Durante a execução, são gerados modelos em formato Keras:

```text
models/
├── cnn_simples.keras
├── transfer_learning_model.keras
└── best_image_classifier.keras
```

O arquivo `best_image_classifier.keras` representa o melhor modelo selecionado com base na comparação final. Nesta execução, o melhor modelo foi o MobileNetV2 com Transfer Learning.

## Limitações

As principais limitações desta etapa são:

- uso de uma única base pública;
- ausência de validação externa;
- presença de possíveis duplicatas;
- ausência de análise de vieses populacionais;
- ausência de revisão clínica formal dos mapas Grad-CAM;
- ausência de máscaras ou bounding boxes para segmentação ou detecção;
- possibilidade de variação nos resultados conforme GPU, versão das bibliotecas e operações não determinísticas.

Essas limitações não invalidam a proposta acadêmica, mas delimitam claramente seu escopo. O resultado deve ser interpretado como experimento de classificação e não como validação clínica.

## Considerações Éticas

Modelos de IA aplicados à saúde exigem uso responsável. Mesmo com bons resultados quantitativos, este projeto não substitui a análise de radiologistas, neurologistas, oncologistas ou outros profissionais de saúde.

O modelo pode apoiar uma triagem inicial ou priorização de análise, mas a decisão final sobre diagnóstico, investigação complementar e conduta clínica deve permanecer sempre com profissionais qualificados.

## Possíveis Melhorias

Como continuidade, recomenda-se:

- remover ou controlar duplicatas antes de novo treinamento;
- validar o modelo em bases externas;
- calibrar probabilidades;
- avaliar outras arquiteturas pré-treinadas;
- revisar os mapas Grad-CAM com especialistas;
- coletar anotações supervisionadas para detecção ou segmentação;
- estudar desempenho por subgrupos e possíveis vieses;
- documentar melhor critérios clínicos e riscos de implantação.


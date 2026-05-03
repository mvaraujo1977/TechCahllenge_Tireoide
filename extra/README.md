# Parte Extra - Visão Computacional com MRI Cerebral

Este diretório contém a parte extra do Tech Challenge, dedicada à aplicação de Visão Computacional em imagens de ressonância magnética cerebral.

## Objetivo

O objetivo é construir um fluxo experimental para classificação de imagens médicas, utilizando o dataset público **Brain Cancer MRI Dataset** do Kaggle.

O notebook realiza:

- Download do dataset via API do Kaggle.
- Inspeção automática da estrutura real dos arquivos.
- Análise exploratória das imagens.
- Preparação dos dados com resize, normalização, divisão treino/validação/teste e data augmentation.
- Treinamento de uma CNN simples.
- Treinamento de um modelo com Transfer Learning e fine-tuning.
- Avaliação dos modelos.
- Visualização interpretável com Grad-CAM.
- Verificação condicional de labels para YOLO.
- Discussão sobre GANs como possibilidade futura.
- Salvamento dos modelos treinados.

## Notebook

```text
extra/
├── 02_visao_computacional_mri_cancer.ipynb
└── README.md
```

## Dataset

O dataset utilizado é:

[Brain Cancer MRI Dataset - Kaggle](https://www.kaggle.com/datasets/orvile/brain-cancer-mri-dataset)

O notebook baixa o dataset diretamente pela API do Kaggle e extrai os arquivos em:

```text
data/raw/brain_cancer_mri/
```

## Execução no Google Colab

1. Abra o notebook `extra/02_visao_computacional_mri_cancer.ipynb` no Google Colab.
2. Execute a célula de instalação de dependências, se necessário.
3. Configure o arquivo `kaggle.json` quando solicitado.
4. Execute as células em ordem.
5. O notebook irá baixar, extrair, inspecionar e preparar automaticamente o dataset.

## YOLO

O notebook só executa fine-tuning com YOLO se encontrar labels compatíveis, como bounding boxes ou estrutura supervisionada adequada.

Caso o dataset possua apenas imagens organizadas por pastas/classes, o notebook não fabrica bounding boxes ou máscaras. Nesse cenário, a localização visual é feita por Grad-CAM, que destaca regiões relevantes para a decisão do modelo, mas não representa segmentação clínica validada.

## Observações Éticas

Este notebook tem finalidade acadêmica e exploratória. Os modelos podem apoiar triagem inicial ou análise preliminar, mas não substituem avaliação de radiologistas, neurologistas, oncologistas ou outros profissionais de saúde.

Grad-CAM indica regiões que influenciaram o modelo, mas não deve ser interpretado como delimitação precisa de tumor. Para detecção ou segmentação clínica real, seriam necessárias anotações supervisionadas feitas por especialistas.

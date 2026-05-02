# 🧠 Tech Challenge - Fase 1

## Sistema de Apoio ao Diagnóstico Médico com Machine Learning

---

## 📌 Descrição do Projeto

Este projeto tem como objetivo desenvolver um modelo de Machine Learning capaz de auxiliar no diagnóstico médico a partir de dados clínicos estruturados.

A solução simula um sistema de apoio à decisão, permitindo identificar automaticamente a presença ou ausência de uma condição médica com base em exames laboratoriais.

---

## 🎯 Objetivo

Construir modelos preditivos capazes de classificar pacientes com base em dados médicos, comparando diferentes algoritmos e avaliando seu desempenho.

---

## 🧩 Construção do Dataset

O dataset final utilizado no projeto (`hypothyroid_final.csv`) não estava originalmente pronto para uso. Foi necessário realizar um processo de construção e consolidação a partir dos arquivos brutos disponibilizados pelo UCI Machine Learning Repository.

As etapas realizadas foram:

* Carregamento do arquivo principal contendo os dados brutos da base de hipotireoidismo
* Identificação e tratamento de valores ausentes, representados por caracteres especiais
* Verificação da existência de um segundo arquivo de dados complementar (`.test`) e, quando disponível, sua combinação com o arquivo principal
* Consolidação de todos os registros em um único DataFrame

---

## 🏷️ Estruturação dos Dados

Após a consolidação dos dados, foi necessário estruturar corretamente o dataset:

* Definição dos nomes das colunas com base no arquivo de descrição (`.names`)
* Quando não foi possível extrair automaticamente os nomes, foi utilizado um mapeamento manual baseado na documentação oficial da UCI
* Padronização dos nomes das variáveis para facilitar o uso no modelo

---

## 🧹 Tratamento Inicial

* Conversão de valores ausentes para formato adequado (`NaN`)
* Organização dos dados em formato tabular estruturado
* Preparação do dataset final para uso nas etapas seguintes

---

## 💾 Dataset Final

Após essas etapas, foi gerado o arquivo final:

👉 `hypothyroid_final.csv`

Este dataset foi utilizado como base para todo o processo de análise e modelagem.

---

## 📊 Características do Dataset

O conjunto de dados contém informações clínicas relevantes, como:

* Idade
* Sexo
* Resultados de exames laboratoriais (TSH, T3, TT4, entre outros)
* Indicadores clínicos (doença, gravidez, uso de medicamentos)

📁 Fonte: UCI Machine Learning Repository

---

## 🔍 Etapas do Projeto

### 1. Exploração de Dados (EDA)

* Análise de valores ausentes
* Estatísticas descritivas
* Visualização da distribuição das variáveis

---

### 2. Pré-processamento

* Remoção de colunas com alta quantidade de valores nulos
* Imputação de valores:

  * Moda para variáveis categóricas
  * Mediana para variáveis numéricas
* Codificação de variáveis categóricas
* Normalização dos dados utilizando técnicas de escalonamento

---

### 3. Separação dos Dados

* Divisão do dataset em treino (80%) e teste (20%)
* Utilização de estratégia para manter a proporção das classes

---

## 🤖 Modelos Utilizados

### 📈 Regressão Logística

* Modelo linear
* Alta interpretabilidade
* Permite entender o impacto das variáveis na decisão

---

### 🌳 Random Forest

* Modelo baseado em múltiplas árvores de decisão
* Capaz de capturar relações não lineares
* Mais robusto para padrões complexos

---

## 📏 Métricas de Avaliação

### 🔥 F1-Score (métrica principal)

A escolha do F1-score se deve ao fato de equilibrar precisão e recall, sendo especialmente importante em problemas médicos, onde tanto falsos positivos quanto falsos negativos têm impacto significativo.

Outras métricas analisadas:

* Accuracy
* Precision
* Recall

---

## 🏆 Resultados

| Modelo              | F1-Score |
| ------------------- | -------- |
| Regressão Logística | X.XX     |
| Random Forest       | X.XX     |

👉 Melhor modelo: **[INSERIR RESULTADO]**

---

## 🧠 Interpretação dos Modelos

* A Regressão Logística permite interpretar diretamente o impacto das variáveis por meio dos coeficientes
* O Random Forest fornece a importância das variáveis com base na sua contribuição para a tomada de decisão

---

## ⚠️ Considerações

* O modelo não substitui a avaliação médica
* Deve ser utilizado como ferramenta de apoio à decisão
* Pode contribuir para maior agilidade na triagem de pacientes

---

## 🚀 Como Executar

1. Clonar o repositório
2. Instalar as dependências
3. Executar o notebook principal do projeto

---

## 📁 Estrutura do Projeto

* Notebook principal com todas as etapas
* Dataset utilizado
* Arquivos auxiliares

---

## 📽️ Demonstração

[INSERIR LINK DO VÍDEO]

---

## 👨‍💻 Autor

Nome de toda a equipe

---

## 📌 Conclusão

O projeto demonstrou a aplicação prática de Machine Learning na área da saúde, evidenciando como modelos preditivos podem auxiliar no processo de diagnóstico, contribuindo para maior eficiência e suporte à tomada de decisão clínica.

---

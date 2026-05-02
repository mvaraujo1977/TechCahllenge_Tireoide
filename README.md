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

## 📊 Dataset

Foi utilizado o dataset de doenças da tireoide (Hypothyroid Dataset), contendo informações como:

* Idade
* Sexo
* Resultados de exames (TSH, T3, TT4, etc.)
* Indicadores clínicos (doença, gravidez, uso de medicação)

📁 Fonte: UCI Machine Learning Repository

---

## 🔍 Etapas do Projeto

### 1. Exploração de Dados (EDA)

* Análise de valores nulos
* Estatísticas descritivas
* Distribuição das variáveis

---

### 2. Pré-processamento

* Remoção da coluna com muitos valores nulos (`TBG`)
* Tratamento de valores ausentes:

  * Moda → variáveis categóricas
  * Mediana → variáveis numéricas
* Codificação de variáveis categóricas (Label Encoding e mapeamento binário)
* Normalização com `StandardScaler`

---

### 3. Separação dos Dados

* Divisão em:

  * Treino (80%)
  * Teste (20%)
* Uso de `stratify` para manter proporção das classes

---

## 🤖 Modelos Utilizados

### 📈 Regressão Logística

* Modelo linear
* Alta interpretabilidade
* Utiliza coeficientes para explicar decisões

---

### 🌳 Random Forest

* Modelo baseado em árvores de decisão
* Captura relações não lineares
* Utiliza ensemble (várias árvores)

---

## 📏 Métricas de Avaliação

A principal métrica utilizada foi:

### 🔥 F1-Score

Motivo:

* Equilibra **Precision** e **Recall**
* Ideal para problemas médicos, onde:

  * Falsos negativos são críticos
  * Falsos positivos também impactam

Outras métricas analisadas:

* Accuracy
* Recall
* Precision

---

## 🏆 Resultados

| Modelo              | F1-Score |
| ------------------- | -------- |
| Regressão Logística | X.XX     |
| Random Forest       | X.XX     |

👉 O modelo com melhor desempenho foi:

**[INSERIR RESULTADO DO SEU CÓDIGO]**

---

## 🧠 Interpretação dos Modelos

### Regressão Logística

* Importância baseada nos coeficientes
* Valores positivos aumentam a probabilidade da classe
* Valores negativos diminuem

---

### Random Forest

* Importância baseada na redução de impureza
* Permite identificar as variáveis mais relevantes para decisão

---

## ⚠️ Considerações Importantes

* O modelo **não substitui o médico**
* Deve ser utilizado como **ferramenta de apoio**
* Pode ajudar na triagem e priorização de pacientes

---

## 🚀 Como Executar o Projeto

### 📦 Pré-requisitos

* Python 3.8+
* Bibliotecas:

  * pandas
  * numpy
  * scikit-learn
  * matplotlib

---

### ▶️ Execução

```bash
git clone https://github.com/seu-repositorio.git
cd seu-repositorio
pip install -r requirements.txt
```

Executar o notebook:

```bash
jupyter notebook
```

---

## 📁 Estrutura do Projeto

```
📂 projeto-ml
 ├── 📄 notebook.ipynb
 ├── 📄 README.md
 ├── 📄 requirements.txt
 ├── 📂 data/
 └── 📂 outputs/
```

---

## 📽️ Demonstração

📺 Vídeo do projeto:
[INSERIR LINK DO YOUTUBE]

---

## 👨‍💻 Autor

Equipe do Tech Challenge

---

## 📌 Conclusão

O projeto demonstrou a aplicação prática de Machine Learning na área da saúde, evidenciando como modelos preditivos podem auxiliar na tomada de decisão clínica, reduzindo tempo e aumentando a eficiência do diagnóstico.

---

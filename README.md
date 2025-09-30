# Proposta de Projeto em Fundamentos de Big Data: Análise Preditiva e de Balanceamento em League of Legends

## 1. Introdução
Este documento detalha a proposta de projeto final para a disciplina de **Fundamentos de Big Data**.  
O projeto utilizará um dos datasets competitivos mais ricos disponíveis publicamente, o **League of Legends Match Data**  
(Kaggle: [datasnaek/league-of-legends](https://www.kaggle.com/datasnaek/league-of-legends)),  
para desenvolver uma solução completa de análise e predição.  

O objetivo é simular um ambiente de análise de e-sports, onde a capacidade de processar grandes volumes de dados de jogos é crucial para o **balanceamento do jogo** e a **estratégia das equipes**.

---

## 2. Objetivo do Projeto
Desenvolver um **pipeline de Big Data** robusto capaz de:

### 🎯 Prever o Resultado da Partida (Match Outcome Prediction)
Criar um modelo de Machine Learning que preveja a equipe vencedora com alta acurácia, utilizando métricas de desempenho no início e meio do jogo (ex: diferença de ouro, controle de objetivos).

### 🔍 Identificar Fatores Críticos de Vitória
Analisar quais campeões, estratégias (itens) e eventos (primeiro dragão, primeiro abate) têm o maior peso estatístico no resultado final da partida.

### ⚖️ Fornecer Insights de Balanceamento
Gerar relatórios que possam auxiliar no balanceamento do jogo, destacando campeões ou estratégias que estão estatisticamente fortes demais (ou fracos demais) em determinados estágios do jogo.

---

## 3. O Pipeline de Big Data: Etapas Obrigatórias
A metodologia do projeto será centrada na construção e documentação do seguinte **pipeline de dados**, utilizando ferramentas apropriadas para um ambiente de Big Data:

### 3.1. Fontes de Dados (Data Sources)
#### 🔹 Fonte Primária
- **Detalhamento:** Dados Competitivos (Semi-Estruturados)  
- **Especificação do Projeto LoL:** Dataset principal do Kaggle (≈30.000 partidas e 500.000 timelines de eventos). Formato: JSON aninhado e estruturado.

#### 🔹 Fonte Secundária
- **Detalhamento:** Dados de Referência (Estruturados)  
- **Especificação do Projeto LoL:** Informações complementares estáticas (ex: estatísticas base de campeões, habilidades) obtidas da Riot Games API (simuladas via arquivo CSV/JSON de lookup ou manual).

#### 🔹 Tipo de Dado
- **Detalhamento:** Variável  
- **Especificação do Projeto LoL:** Dados de alta cardinalidade e dimensionalidade (centenas de métricas por partida), variando de numéricos a categóricos.

---

### 3.2. Ingestão (Ingestion)
#### 🔹 Processo
- **Detalhamento:** Batch (Lotes)  
- **Especificação do Projeto LoL:** Ingestão em modo batch devido à natureza estática do dataset.

#### 🔹 Ferramenta Principal
- **Detalhamento:** Apache Spark (PySpark)  
- **Especificação do Projeto LoL:** Uso da leitura de JSON distribuída e eficiente via Spark.

#### 🔹 Detalhe do Processo
- **Detalhamento:** Script  
- **Especificação do Projeto LoL:** Script em PySpark para leitura dos JSONs aninhados, inferência de schema e criação de DataFrames distribuídos.

---

### 3.3. Transformação (Transformation)
Etapa crítica e intensiva, responsável pelo tratamento dos dados de timeline.

#### 🔹 Ferramenta Principal
- **Detalhamento:** Apache Spark (PySpark/Spark SQL)  
- **Especificação do Projeto LoL:** Essencial para limpeza e feature engineering distribuída.

#### 🔹 Limpeza e Normalização
- **Detalhamento:** Tratamento de Dados  
- **Especificação do Projeto LoL:** Tratamento de nulos, ajuste de tipos (numéricos, categóricos), e padronização.

#### 🔹 Feature Engineering
- **Detalhamento:** Criação de Métricas  
- **Especificação do Projeto LoL:** Desaninhamento de JSON (extração de Ouro/Objetivos aos 10/15 minutos), cálculo de métricas (KDA, Taxa de Participação em Abates).

#### 🔹 Agregação
- **Detalhamento:** Estrutura de ML  
- **Especificação do Projeto LoL:** Transformar as 10 linhas de jogador por partida em uma única linha de matriz de features, com foco na diferença entre Time 1 e Time 2.

---

### 3.4. Carregamento (Loading)
#### 🔹 Processo
- **Detalhamento:** Exportação do DataFrame  
- **Especificação do Projeto LoL:** Exportação do DataFrame final (matriz de features) para análise.

#### 🔹 Ferramenta Principal
- **Detalhamento:** Spark Write  
- **Especificação do Projeto LoL:** Escrita em formato colunar otimizado (Parquet ou Delta Lake).

---

### 3.5. Destino (Destination)
#### 🔹 Armazenamento
- **Detalhamento:** Data Lake  
- **Especificação do Projeto LoL:** Simulação de Data Lake via arquivos Parquet contendo features de Machine Learning.

#### 🔹 Consumo/Visualização
- **Detalhamento:** Interface de BI  
- **Especificação do Projeto LoL:** Aplicação em Python (Streamlit ou Dash) para visualização dos insights e métricas principais.

---

## 4. Modelagem (Etapa Adicional de Valor)
#### 🔹 Objetivo
- **Detalhamento:** Classificação  
- **Especificação do Projeto LoL:** Classificação binária para prever o time vencedor (Vitória/Derrota).

#### 🔹 Modelo Sugerido
- **Detalhamento:** Classificador Distribuído  
- **Especificação do Projeto LoL:** Gradient Boosting Machine (GBM) (XGBoost ou LightGBM) ou Regressão Logística, com Spark MLlib.

#### 🔹 Métricas
- **Detalhamento:** Avaliação do Modelo  
- **Especificação do Projeto LoL:** Acurácia, F1-Score e Curva ROC.

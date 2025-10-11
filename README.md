# Projeto de Análise e Predição em League of Legends

## 📘 Descrição do Projeto
Este projeto foi desenvolvido como parte da disciplina **Tópicos Contemporâneos 3**, com o objetivo de aplicar conceitos de **armazenamento, transformação e análise de dados** sobre partidas ranqueadas do jogo **League of Legends (LoL)**.  

A partir do dataset analisado, o grupo realizou um processo de **pré-processamento e modelagem preditiva**, utilizando o algoritmo **Random Forest Classifier** para prever resultados com base em variáveis do jogo.

---

## 🎯 Objetivo
Criar um **modelo de predição** capaz de estimar o resultado de partidas de League of Legends com base em estatísticas coletadas de jogos ranqueados.

---

## 📂 Fonte dos Dados
O dataset utilizado está disponível publicamente no Kaggle:  
🔗 [League of Legends Ranked Games](https://www.kaggle.com/datasets)

---

## 🧰 Ferramentas Utilizadas
As principais ferramentas e bibliotecas empregadas foram:

- **Google Colab** → ambiente de desenvolvimento e execução do projeto  
- **Python** → linguagem de programação principal  
- **Pandas** → manipulação e tratamento de dados  
- **Scikit-learn (Sklearn)** → implementação e treino do modelo de *Random Forest Classifier*  

---

## 👥 Equipe
Projeto desenvolvido pelo grupo da disciplina **Tópicos Contemporâneos 3**.

- **Antônio Neto**
- **Davi César**
- **João Ricardo**

---

## 📊 Resultado Esperado
Um modelo de **classificação preditiva** baseado em aprendizado de máquina, capaz de auxiliar na compreensão dos fatores que mais influenciam a vitória em partidas ranqueadas de *League of Legends*.

---

## 🏗️ Arquitetura do Projeto

A arquitetura do projeto foi estruturada para contemplar as três principais etapas do processo de ciência de dados: **armazenamento, transformação** e **análise preditiva**.  

### 1. Ingestão e Armazenamento dos Dados
Os dados foram obtidos a partir do dataset **League of Legends Ranked Games** disponível no Kaggle.  
O conjunto de dados foi importado e armazenado em ambiente **Google Colab**, utilizando **Pandas** para leitura e manipulação em memória.  

- **Formato original:** CSV  
- **Carregamento:** `pandas.read_csv()`  
- **Armazenamento temporário:** DataFrame Pandas  

---

### 2. Limpeza e Transformação dos Dados
Antes da análise, o dataset passou por uma série de transformações para garantir sua consistência e preparar os dados para a modelagem.

As principais etapas foram:

- **Remoção de duplicatas:**  
  Identificação de registros com o mesmo `gameId`. Para evitar distorções, foi mantida apenas **uma instância única** de cada jogo.

- **Filtragem das colunas relevantes:**  
  Como o objetivo final era prever o time vencedor, todas as colunas desnecessárias foram removidas, mantendo apenas:
  - As colunas referentes aos **campeões utilizados** nas partidas;
  - A coluna que indica **qual time venceu** (variável alvo).

- **Análise dos campeões mais frequentes:**  
  Foi realizada uma contagem para identificar **os 10 campeões mais utilizados** nas partidas.  
  Essa análise serviu tanto para explorar o dataset quanto para compreender quais variáveis poderiam ter maior relevância na predição.

---

### 3. Análise e Modelagem Preditiva
Com o dataset limpo e filtrado, iniciou-se a etapa de **modelagem com aprendizado de máquina**.

- **Algoritmo utilizado:** Random Forest Classifier (da biblioteca Scikit-learn)  
- **Objetivo do modelo:** prever o **time vencedor** com base na composição de campeões.  

O modelo foi treinado e testado dentro do ambiente **Google Colab**, utilizando as bibliotecas:
- `sklearn.ensemble.RandomForestClassifier`  
- `sklearn.model_selection` para divisão dos dados (treino e teste)  
- `sklearn.metrics` para avaliação de desempenho  

---

### 🧩 Resumo do Fluxo de Dados
1. **Coleta:** Dataset do Kaggle (League of Legends Ranked Games)  
2. **Armazenamento:** Google Colab + DataFrame Pandas  
3. **Transformação:**  
   - Remoção de duplicatas (`gameId`)  
   - Seleção de colunas relevantes  
   - Análise de campeões mais usados  
4. **Modelagem:** Random Forest Classifier  
5. **Saída:** Predição do time vencedor e métricas de desempenho  



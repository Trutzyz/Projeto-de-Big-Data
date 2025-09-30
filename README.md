Proposta de Projeto em Fundamentos de Big Data: Análise Preditiva e de Balanceamento em League of Legends
1. Introdução
Este documento detalha a proposta de projeto final para a disciplina de Fundamentos de Big Data. O projeto utilizará um dos datasets competitivos mais ricos disponíveis publicamente, o League of Legends Match Data (Kaggle: datasnaek/league-of-legends), para desenvolver uma solução completa de análise e predição. O objetivo é simular um ambiente de análise de e-sports, onde a capacidade de processar grandes volumes de dados de jogos é crucial para o balanceamento do jogo e a estratégia das equipes.

2. Objetivo do Projeto
Desenvolver um pipeline de Big Data robusto capaz de:

Prever o Resultado da Partida (Match Outcome Prediction): Criar um modelo de Machine Learning que preveja a equipe vencedora com alta acurácia, utilizando métricas de desempenho no início e meio do jogo (ex: diferença de ouro, controle de objetivos).

Identificar Fatores Críticos de Vitória: Analisar quais campeões, estratégias (itens) e eventos (primeiro dragão, primeiro abate) têm o maior peso estatístico no resultado final da partida.

Fornecer Insights de Balanceamento: Gerar relatórios que possam auxiliar no balanceamento do jogo, destacando campeões ou estratégias que estão estatisticamente fortes demais (ou fracos demais) em determinados estágios do jogo.

3. O Pipeline de Big Data: Etapas Obrigatórias
A metodologia do projeto será centrada na construção e documentação do seguinte pipeline de dados, utilizando ferramentas apropriadas para um ambiente de Big Data:

3.1. Fontes de Dados (Data Sources)
Detalhamento

Especificação do Projeto LoL

Fonte Primária

Dados Competitivos (Semi-Estruturados): O dataset principal do Kaggle (aproximadamente 30.000 partidas e 500.000 timelines de eventos). O formato é majoritariamente JSON aninhado e estruturado.

Fonte Secundária

Dados de Referência (Estruturados): Informações complementares estáticas (ex: estatísticas base de campeões, habilidades) que seriam obtidas da Riot Games API (simuladas por um arquivo CSV/JSON de lookup ou manual).

Tipo de Dado

Dados de alta cardinalidade e dimensionalidade (centenas de métricas por partida), variando de numéricos a categóricos.

3.2. Ingestão (Ingestion)
Detalhamento

Especificação do Projeto LoL

Processo

Batch (Lotes): Dada a natureza estática do dataset principal, a ingestão será realizada em modo batch.

Ferramenta Principal

Apache Spark (PySpark): Utilizaremos a funcionalidade de leitura de JSON do Spark para carregar os grandes arquivos da fonte de dados de maneira distribuída e eficiente.

Processo

Um script em PySpark será responsável por ler os arquivos JSON aninhados, inferir o schema inicial e criar DataFrames distribuídos para as próximas etapas.

3.3. Transformação (Transformation)
Esta é a etapa mais crítica e intensiva, onde a complexidade dos dados de timeline é resolvida.

Detalhamento

Especificação do Projeto LoL

Ferramenta Principal

Apache Spark (PySpark/Spark SQL): Essencial para a limpeza e feature engineering distribuída.

Limpeza e Normalização

Tratamento de Nulos/Ausentes: Preenchimento ou remoção de dados inconsistentes ou faltantes (ex: campeões não reconhecidos). Ajuste de Tipos de Dados: Garantir que colunas numéricas (ouro, abates) sejam formatadas corretamente.

Feature Engineering

Desaninhamento de JSON: Extrair dados cruciais do JSON aninhado de timelines (ex: Ouro por Posição aos 10 minutos, Contagem de Objetivos aos 15 minutos). Cálculo de Métricas: Criação de métricas de desempenho (ex: KDA, Taxa de Participação em Abates, Contagem de Wards).

Agregação

Estrutura de ML: Transformar as 10 linhas de jogador por partida em uma única linha de matriz de features para o modelo preditivo, focando na diferença de métricas entre o Time 1 e o Time 2.

3.4. Carregamento (Loading)
Detalhamento

Especificação do Projeto LoL

Processo

O Spark carregará o DataFrame final, que contém a matriz de features limpa e agregada.

Ferramenta Principal

Spark Write to Parquet/Delta Lake: Utilizar a funcionalidade de escrita do Spark para exportar os dados para um formato colunar otimizado para análise.

3.5. Destino (Destination)
Detalhamento

Especificação do Projeto LoL

Armazenamento

Data Lake (Simulado via Arquivos Parquet): O local final onde os dados prontos para consumo (Machine Learning Features) serão armazenados. O formato Parquet garante compressão e consultas rápidas.

Consumo/Visualização

Interface de BI (Streamlit ou Dash): Uma aplicação simples em Python será desenvolvida para carregar os dados Parquet/Delta Lake e visualizar as principais conclusões (ex: acurácia do modelo, ranking de impacto de campeões).

4. Modelagem (Etapa Adicional de Valor)
Detalhamento

Especificação do Projeto LoL

Objetivo

Classificação binária: Prever Time Vencedor (Vitória/Derrota).

Modelo Sugerido

Gradient Boosting Machine (GBM) (ex: XGBoost ou LightGBM) ou Regressão Logística, utilizando a biblioteca Spark MLlib para treinamento distribuído.

Métricas

Acurácia, F1-Score e Curva ROC.
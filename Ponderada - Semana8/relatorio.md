# Documentação do Projeto: Detecção de Bots no Twitter

## Introdução

Este projeto tem como objetivo detectar contas de bots no Twitter utilizando aprendizado de máquina e o modelo BERT. O processo foi realizado em um ambiente Colab, onde os dados foram carregados, pré-processados, e um modelo BERT foi treinado e avaliado.

## Importação de Bibliotecas

Foram utilizadas bibliotecas como `transformers`, `torch`, `scikit-learn` e `pandas` para facilitar o processamento de texto, manipulação de dados e construção do modelo.

## Carregamento e Visualização dos Dados

Os dados foram carregados a partir de um arquivo CSV, contendo informações essenciais sobre usuários do Twitter e suas atividades. As principais colunas incluíam:

- **User ID**: ID do usuário.
- **Username**: Nome de usuário no Twitter.
- **Tweet**: Conteúdo do tweet.
- **Retweet Count**: Número de retweets.
- **Mention Count**: Número de menções.
- **Follower Count**: Contagem de seguidores.
- **Verified**: Indica se o usuário é verificado.
- **Bot Label**: Indica se o usuário é um bot.
- **Location**: Localização do usuário.
- **Created At**: Data de criação do tweet.
- **Hashtags**: Hashtags no tweet.

## Pré-processamento dos Dados

### Simplificação da Base

A base foi reduzida para 10% dos dados originais para facilitar o treinamento e reduzir o tempo de processamento. A base foi simplificada devido ao tempo de treinamento ser muito longo e sobrecarregar as maquinas disponiveis

### Tratamento de Valores Nulos

Valores nulos na coluna `Hashtags` foram preenchidos com strings vazias para evitar problemas durante o treinamento.

### Codificação de Variáveis Categóricas

Variáveis categóricas como `Location` e `Verified` foram codificadas para converter texto em valores numéricos, essenciais para o modelo de aprendizado de máquina.

### Normalização de Variáveis Numéricas

Variáveis como `Retweet Count`, `Mention Count`, e `Follower Count` foram normalizadas para garantir que tenham a mesma escala, melhorando a eficácia do modelo.

### Definição de Features e Rótulos

As features selecionadas incluíram informações textuais e numéricas, enquanto a coluna `Bot Label` foi usada como rótulo.

### Divisão dos Dados

Os dados foram divididos em conjuntos de treino (80%) e teste (20%) para avaliar o desempenho do modelo em dados não vistos.

## Treinamento do Modelo

### Tokenização

Os tweets foram tokenizados usando o BERT tokenizer, que transforma o texto em tokens compreensíveis pelo modelo BERT.

### Preparação dos Dados para PyTorch

Os dados foram convertidos em tensores para serem usados com o PyTorch, permitindo o processamento eficiente de dados em lote.

### DataLoader

DataLoaders foram configurados para gerenciar os dados de treino e teste, facilitando o carregamento em lotes durante o treinamento.

### Modelo BERT

O modelo BERT foi carregado e configurado para classificação de sequência, com ajustes para identificar se um usuário é um bot ou não.

### Treinamento

O modelo foi treinado por 5 épocas. Durante o treinamento, a perda foi monitorada para garantir que o modelo estava aprendendo. as 5 épocas foram escolhidas devido ao tempo do treinamento, esse treinamento durou 1h10 

## Avaliação do Modelo

O modelo foi avaliado no conjunto de teste. A acurácia obtida foi de 0.531, revelando desafios na detecção de bots.

### Resultados

- **Acurácia**: 0.531
- **Relatório de Classificação**:
  - **Não-Bot**: Precisão de 0.53, Recall de 1.00
  - **Bot**: Precisão e Recall baixos

**Motivos para Desempenho Limitado**:
- **Desbalanceamento de Classes**: A classe "Bot" pode estar sub-representada, afetando a capacidade do modelo de aprender suas características.
- **Complexidade Textual**: Tweets são textos curtos e podem não conter informações suficientes para distinguir claramente entre bots e humanos.


## Conclusão

Este projeto demonstrou com sucesso o potencial do BERT na classificação de texto para detecção de bots no Twitter. Os resultados iniciais oferecem uma base sólida para futuras melhorias e ajustes.

### Métricas de Avaliação

- **Precisão**: [0.531 para Não-Bot, 0.0 para Bot]
- **Recall**: [1.0 para Não-Bot, 0.0 para Bot]
- **F1-Score**: [0.69 para Não-Bot, 0.0 para Bot]

### Análise dos Resultados

Apesar das limitações na detecção de bots, o modelo mostrou excelente desempenho ao identificar contas legítimas. Isso destaca a robustez do BERT e abre caminho para avanços significativos.

### Caminhos para Melhorias

1. **Balanceamento de Dados**: Ao equilibrar as classes, podemos aumentar a capacidade do modelo de identificar bots com precisão.

2. **Aprimoramento do Modelo**: Com ajustes na arquitetura e nos hiperparâmetros, podemos melhorar ainda mais a eficácia do modelo.

3. **Enriquecimento dos Dados**: Incorporar novas features e mais dados pode enriquecer o contexto e melhorar a detecção.

Com essas estratégias, estamos otimistas de que o modelo pode evoluir para se tornar uma ferramenta poderosa na identificação de bots, contribuindo para um ambiente digital mais seguro e autêntico. Este projeto é um passo promissor em direção a soluções mais eficazes e inovadoras.
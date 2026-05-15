# Pré-Processamento de Dados e Análise Exploratória — Temperatura UH Prensa

## Alunos

- Alberto Zilio
- Lucas Carvalho Steffens
- Roni Pereira


## Tema da atividade

Técnicas de pré-processamento de dados aplicadas a um dataset real de temperatura da unidade hidráulica de uma prensa industrial.

## Repositório

Este repositório contém o desenvolvimento da atividade prática de pré-processamento de dados utilizando Python, pandas, scikit-learn e Google Colab.

Dataset utilizado:

```text
Data/Status_Temperatura_UH_Prensa (2).xlsx
```

Notebook principal:

```text
Analise_Exploratoria_Temperatura_UH_Prensa_Colab.ipynb
```

---

## Objetivo da análise

O objetivo desta atividade é aplicar técnicas de pré-processamento de dados e análise exploratória sobre um dataset real de temperatura coletada em uma unidade hidráulica de prensa.

A análise busca demonstrar as principais etapas de preparação dos dados antes de uma possível aplicação em modelos analíticos ou preditivos.

As atividades desenvolvidas contemplam:

- Importação do dataset a partir do GitHub;
- Leitura de arquivo Excel no Google Colab;
- Inspeção inicial da estrutura dos dados;
- Limpeza e tratamento inicial da base;
- Padronização dos nomes das colunas;
- Identificação e tratamento de valores faltantes;
- Conversão de tipos de dados;
- Correção de inconsistências na escala da temperatura;
- Remoção de registros inválidos;
- Verificação de duplicidades;
- Análise exploratória de dados;
- Criação de variáveis derivadas;
- Normalização com `MinMaxScaler`;
- Padronização com `StandardScaler`;
- Transformação categórica com `OneHotEncoder`;
- Dummy encoding com `pandas.get_dummies`;
- Exportação dos resultados tratados.

A proposta está alinhada com a atividade prática da Aula 8, que solicita tratamento de dados faltantes, aplicação de transformações numéricas com `MinMaxScaler` e `StandardScaler`, transformações categóricas com `OneHotEncoder` e dummy encoding, além de uma AED — Análise Exploratória de Dados — sobre o dataset escolhido.

---

## Dataset utilizado

O dataset utilizado nesta atividade corresponde a registros de temperatura da unidade hidráulica de uma prensa.

O arquivo está armazenado no repositório dentro da pasta:

```text
Data/
```

Arquivo:

```text
Status_Temperatura_UH_Prensa (2).xlsx
```

A base contém registros de data/hora e valores de temperatura, permitindo avaliar o comportamento térmico do equipamento ao longo do tempo.

---

## Estrutura sugerida do repositório

```text
pre-processamento_atividade_02-N2/
│
├── Data/
│   └── Status_Temperatura_UH_Prensa (2).xlsx
│
├── Analise_Exploratoria_Temperatura_UH_Prensa_Colab.ipynb
│
├── README.md
│
├── LICENSE
│
└── .gitattributes
```

---

## Tecnologias utilizadas

### Linguagem

- Python

### Ambiente

- Google Colab

### Bibliotecas principais

- pandas
- numpy
- matplotlib
- scikit-learn
- openpyxl
- pathlib
- re
- subprocess

---

## Etapas desenvolvidas no notebook

### 1. Importação das bibliotecas

Inicialmente são importadas as bibliotecas necessárias para manipulação dos dados, análise numérica, geração de gráficos e aplicação das técnicas de pré-processamento.

Principais bibliotecas utilizadas:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from sklearn.preprocessing import MinMaxScaler, StandardScaler, OneHotEncoder
```

---

### 2. Importação do dataset a partir do GitHub

O notebook realiza a clonagem do repositório diretamente no ambiente do Google Colab.

A planilha é carregada a partir da pasta:

```text
Data/
```

Caso o repositório esteja privado, é necessário utilizar um token do GitHub no Colab Secrets com o nome:

```text
GITHUB_TOKEN
```

---

### 3. Leitura da planilha Excel

Após a clonagem do repositório, o notebook localiza automaticamente o arquivo `.xlsx` dentro da pasta `Data`.

Em seguida, a planilha é carregada para um DataFrame do pandas.

Essa etapa permite transformar os dados da planilha em uma estrutura tabular adequada para análise.

---

### 4. Inspeção inicial da base

Nesta etapa são avaliadas informações gerais da base de dados, como:

- Quantidade de linhas;
- Quantidade de colunas;
- Nomes das colunas;
- Tipos de dados;
- Primeiras linhas;
- Últimas linhas.

Essa inspeção inicial é importante para compreender a estrutura dos dados e identificar possíveis necessidades de tratamento.

---

### 5. Tratamento inicial dos dados

Nesta etapa são removidas:

- Linhas totalmente vazias;
- Colunas totalmente vazias.

Esse procedimento evita que informações sem utilidade prejudiquem as etapas seguintes da análise.

---

### 6. Padronização dos nomes das colunas

Os nomes das colunas são padronizados para facilitar o uso no código.

A padronização remove ou ajusta:

- Espaços;
- Letras maiúsculas;
- Caracteres especiais;
- Barras;
- Pontos;
- Hífens.

Exemplo:

```text
Value Float
```

pode ser transformado em:

```text
value_float
```

---

### 7. Verificação de valores faltantes

A base é analisada para identificar valores ausentes.

Para cada coluna são calculados:

- Quantidade de valores faltantes;
- Percentual de valores faltantes.

O tratamento de valores faltantes é uma etapa essencial do pré-processamento, pois dados ausentes podem prejudicar análises estatísticas e modelos preditivos.

---

### 8. Identificação das colunas principais

O notebook identifica as principais colunas utilizadas na análise:

- Coluna de data/hora;
- Coluna de temperatura.

Essas colunas são fundamentais para avaliar o comportamento da temperatura ao longo do tempo.

---

### 9. Conversão dos tipos de dados

Nesta etapa são realizadas conversões importantes:

- A coluna de data/hora é convertida para o tipo `datetime`;
- A coluna de temperatura é convertida para tipo numérico.

Esse tratamento é necessário porque dados importados de planilhas podem ser interpretados inicialmente como texto.

---

### 10. Correção da escala da temperatura

Foram tratadas possíveis inconsistências na escala dos valores de temperatura.

Em alguns casos, valores como:

```text
395
```

podem representar:

```text
39.5 °C
```

Por isso, o notebook aplica uma regra de correção para ajustar valores aparentemente fora da escala esperada.

---

### 11. Remoção de registros inválidos

Após as conversões, são removidos registros sem:

- Data/hora válida;
- Temperatura válida.

Esses registros não são adequados para a análise temporal da temperatura.

---

### 12. Tratamento de dados faltantes

Esta etapa atende diretamente à atividade prática de tratamento de valores faltantes.

Foram testadas duas estratégias:

#### Exclusão de registros faltantes

Nesta abordagem, os registros com valores ausentes são removidos.

Vantagem:

- Simples de aplicar.

Desvantagem:

- Pode reduzir a quantidade de dados disponíveis.

#### Preenchimento com mediana

Nesta abordagem, valores faltantes de temperatura são preenchidos com a mediana da coluna.

Vantagem:

- Mantém a quantidade de registros;
- É menos sensível a valores extremos do que a média.

Essa prática atende ao item da atividade que solicita excluir e/ou preencher valores faltantes em um DataFrame.

---

### 13. Verificação de duplicidades

O notebook verifica se existem registros duplicados na base.

Caso sejam encontrados, os registros duplicados podem ser removidos para evitar distorções na análise.

---

### 14. Estatísticas descritivas

São calculadas estatísticas da temperatura, como:

- Média;
- Mediana;
- Mínimo;
- Máximo;
- Desvio padrão;
- Variância;
- Quartis.

Essas informações permitem compreender o comportamento geral da temperatura da unidade hidráulica.

---

### 15. Histograma da temperatura

Foi gerado um histograma para visualizar a distribuição dos valores de temperatura.

O histograma ajuda a identificar:

- Faixas de temperatura mais frequentes;
- Concentração dos dados;
- Possíveis assimetrias;
- Comportamentos fora do padrão.

---

### 16. Boxplot da temperatura

Foi gerado um boxplot para analisar a dispersão dos dados e identificar possíveis outliers.

O boxplot permite visualizar:

- Mediana;
- Quartis;
- Amplitude dos dados;
- Valores extremos.

---

### 17. Criação de faixas de temperatura

A temperatura, originalmente numérica e contínua, foi transformada em uma variável categórica por meio de faixas.

Exemplo de faixas:

```text
0 a 20 °C
20 a 30 °C
30 a 40 °C
40 a 50 °C
50 a 60 °C
60 a 70 °C
Acima de 70 °C
```

Essa etapa representa uma forma de discretização, transformando uma variável contínua em categorias interpretáveis.

---

### 18. Transformações numéricas

A atividade solicita o uso de transformações numéricas com `MinMaxScaler` e `StandardScaler`.

Essas técnicas são importantes em contextos de análise de dados e aprendizado de máquina, especialmente quando os algoritmos são sensíveis à escala dos atributos.

#### 18.1 Normalização com MinMaxScaler

A normalização foi aplicada à variável de temperatura.

O `MinMaxScaler` transforma os valores para o intervalo entre 0 e 1.

Exemplo de coluna gerada:

```text
temperatura_normalizada
```

#### 18.2 Padronização com StandardScaler

A padronização foi aplicada à variável de temperatura.

O `StandardScaler` transforma os dados para uma escala com:

- Média próxima de 0;
- Desvio padrão próximo de 1.

Exemplo de coluna gerada:

```text
temperatura_padronizada
```

---

### 19. Transformações categóricas

A atividade solicita a aplicação de transformações categóricas utilizando `OneHotEncoder` e dummy encoding.

Essas técnicas transformam variáveis categóricas em colunas binárias.

#### 19.1 OneHotEncoder

Foi aplicado `OneHotEncoder` sobre a variável categórica:

```text
faixa_temperatura
```

O resultado é um conjunto de colunas binárias representando cada faixa de temperatura.

Exemplo:

```text
faixa_temperatura_20 a 30 °C
faixa_temperatura_30 a 40 °C
faixa_temperatura_40 a 50 °C
```

#### 19.2 Dummy Encoding

Também foi aplicado dummy encoding utilizando:

```python
pd.get_dummies()
```

A principal diferença é que, no dummy encoding, pode-se remover uma das categorias por meio do parâmetro:

```python
drop_first=True
```

Essa técnica pode ser útil para reduzir multicolinearidade em modelos de regressão.

---

### 20. Análise de limites críticos

Foram avaliados registros acima de limites específicos de temperatura, como:

- 40 °C;
- 45 °C;
- 50 °C;
- 55 °C;
- 60 °C;
- 65 °C;
- 70 °C.

Para cada limite são calculados:

- Quantidade de registros acima do limite;
- Percentual em relação ao total;
- Tempo estimado acima do limite.

Essa análise permite identificar possíveis condições críticas de operação do equipamento.

---

### 21. Análise diária

Os dados foram agrupados por dia para identificar o comportamento diário da temperatura.

Foram calculados:

- Quantidade de registros por dia;
- Temperatura média diária;
- Temperatura mínima diária;
- Temperatura máxima diária.

Essa análise permite identificar dias com maior aquecimento da unidade hidráulica.

---

### 22. Análise por hora do dia

Os dados também foram agrupados por hora.

Foram analisadas:

- Temperatura média por hora;
- Temperatura máxima por hora;
- Quantidade de registros por hora.

Essa análise permite verificar se existem períodos do dia com maior tendência de aquecimento.

---

### 23. Identificação de falhas na coleta

Foi calculado o intervalo de tempo entre medições consecutivas.

Quando o intervalo entre duas medições é muito grande, pode representar uma possível falha ou interrupção na coleta de dados.

O critério utilizado foi identificar gaps maiores que 60 segundos.

---

### 24. Análise de evento crítico acima de 60 °C

Foi criada uma análise específica para registros com temperatura maior ou igual a 60 °C.

Essa análise permite verificar:

- Quantidade de registros críticos;
- Primeiro registro crítico;
- Último registro crítico;
- Temperatura máxima durante o evento crítico.

---

### 25. Exportação dos resultados

Ao final, os resultados são exportados para um arquivo Excel contendo diferentes abas, como:

- Estatísticas;
- Valores faltantes;
- Análise diária;
- Análise por hora;
- Limites críticos;
- Falhas de coleta;
- Dados pré-processados.

Arquivo de saída sugerido:

```text
resultados_analise_temperatura_uh_prensa.xlsx
```

---

## Principais arquivos gerados

Durante a execução do notebook podem ser gerados arquivos de saída, como:

```text
resultados_analise_temperatura_uh_prensa.xlsx
relatorio_analise_temperatura_uh_prensa.docx
```

Esses arquivos podem ser utilizados como apoio para documentação, entrega da atividade ou análise posterior.

---

## Como executar no Google Colab

### 1. Abrir o notebook no Colab

Abra o arquivo:

```text
Analise_Exploratoria_Temperatura_UH_Prensa_Colab.ipynb
```

### 2. Executar as células em sequência

Execute as células do notebook na ordem apresentada.

### 3. Repositório privado

Caso o repositório esteja privado, configure o token do GitHub no Colab Secrets.

Nome do segredo:

```text
GITHUB_TOKEN
```

O token deve possuir permissão de leitura do repositório.

### 4. Conferir a pasta Data

O notebook espera encontrar o dataset na pasta:

```text
Data/
```

Com o arquivo:

```text
Status_Temperatura_UH_Prensa (2).xlsx
```

---

## Requisitos

Para executar a análise, são necessárias as seguintes bibliotecas:

```text
pandas
numpy
matplotlib
scikit-learn
openpyxl
python-docx
```

No Google Colab, a maioria dessas bibliotecas já está disponível. Caso alguma biblioteca esteja ausente, ela pode ser instalada com:

```python
!pip install nome-da-biblioteca
```

Exemplo:

```python
!pip install python-docx
```

---

## Exemplo de instalação de dependências

```python
!pip install pandas numpy matplotlib scikit-learn openpyxl python-docx
```

---

## Resultados esperados

Ao final da execução do notebook, espera-se obter:

- Dataset carregado corretamente a partir do GitHub;
- Dados limpos e organizados;
- Colunas padronizadas;
- Valores faltantes identificados e tratados;
- Temperatura convertida para formato numérico;
- Registros inválidos removidos;
- Duplicidades verificadas;
- Estatísticas descritivas da temperatura;
- Gráficos de distribuição e boxplot;
- Faixas de temperatura criadas;
- Temperatura normalizada;
- Temperatura padronizada;
- Variáveis categóricas transformadas em colunas binárias;
- Análises por dia e por hora;
- Identificação de possíveis falhas de coleta;
- Exportação dos dados e resultados tratados.

---

## Conclusão

Esta atividade demonstrou a aplicação prática de técnicas de pré-processamento de dados em um dataset industrial real.

O uso de dados de temperatura da unidade hidráulica de uma prensa permitiu aplicar conceitos fundamentais de preparação de dados, como limpeza, tratamento de valores ausentes, correção de inconsistências, transformação numérica, transformação categórica e análise exploratória.

Além disso, a análise possibilitou interpretar o comportamento térmico do equipamento ao longo do tempo, identificar possíveis períodos críticos e preparar a base para futuras aplicações em manutenção preditiva, monitoramento industrial ou modelagem analítica.

---

## Observações

Este projeto foi desenvolvido para fins acadêmicos, como parte da atividade prática de revisão sobre técnicas de pré-processamento de dados.

O notebook foi estruturado para ser executado no Google Colab, utilizando o dataset armazenado no próprio repositório GitHub.

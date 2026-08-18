# Análise e Tratamento de Dados de Produção de Etanol

Projeto desenvolvido em Python para **identificação, tratamento e análise exploratória de dados relacionados à produção de etanol no Brasil**, utilizando dados referentes aos estados brasileiros entre 2019 e 2023.

O projeto contempla etapas de **limpeza de dados, identificação de inconsistências, tratamento de valores ausentes, detecção de outliers e análise gráfica**, buscando obter informações sobre a distribuição e evolução da produção de etanol hidratado e anidro.

## Objetivos

* Identificar valores ausentes no dataset;
* Detectar registros duplicados;
* Identificar e tratar outliers;
* Detectar valores negativos nas variáveis de produção;
* Validar anos, meses, regiões e estados;
* Padronizar nomes dos estados brasileiros;
* Tratar valores ausentes;
* Analisar a produção de etanol por estado e região;
* Identificar estados com maior produção;
* Avaliar a evolução da produção ao longo dos anos;
* Produzir visualizações para auxiliar na interpretação dos dados.

## Dataset

O dataset utilizado contém informações mensais sobre a produção de combustíveis nos estados brasileiros.

**Período analisado:** 2019–2023

Entre as principais variáveis utilizadas estão:

* `Estado`
* `Região`
* `Mês/Ano`
* `Produção Etanol Hidratado(m³/d)`
* `Produção Etanol Anidro (m³/d)`

Dataset utilizado:

https://raw.githubusercontent.com/ccalmendra/ciencia-dados/refs/heads/main/dados/ap2-combustivel-producao.csv

## Tecnologias utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Regular Expressions (`re`)
* Unicode (`unicodedata`)

## Etapas do projeto

### 1. Identificação de problemas

Inicialmente, o dataset é analisado para identificar possíveis problemas de qualidade.

São verificadas:

* Linhas com valores ausentes;
* Quantidade de valores ausentes por coluna;
* Registros duplicados;
* Outliers;
* Valores negativos;
* Meses inválidos;
* Anos inválidos;
* Regiões inválidas;
* Estados inválidos ou não padronizados.

Também são extraídos os valores de **ano** e **mês** a partir da coluna `Mês/Ano`.

### 2. Tratamento dos dados

Após a identificação dos problemas, é criado um novo DataFrame para preservar os dados originais.

Os principais tratamentos realizados são:

#### Valores ausentes

Os valores ausentes nas colunas de produção são preenchidos utilizando a **mediana** da respectiva coluna.

Essa abordagem reduz a influência de valores extremos sobre o preenchimento.

#### Duplicatas

São removidos registros duplicados considerando a combinação:

`Estado + Ano + Mês`

#### Outliers

Os outliers das variáveis de produção são identificados utilizando o método do **Intervalo Interquartil (IQR)**.

Os limites utilizados são:

```text
Limite inferior = Q1 - 1,5 × IQR
Limite superior = Q3 + 1,5 × IQR
```

Os valores que ultrapassam esses limites são substituídos pelo respectivo limite.

#### Estados

Os nomes dos estados são padronizados utilizando um dicionário com as siglas e os nomes oficiais dos estados brasileiros.

Também é realizada a normalização de texto para permitir o reconhecimento de nomes com diferenças de acentuação ou formatação.

#### Ano e mês

Os valores de ano e mês são extraídos utilizando expressões regulares.

Também são realizadas validações para verificar se os valores estão dentro dos períodos esperados.

#### Regiões

Os valores da coluna `Região` são padronizados, removendo espaços extras e convertendo os valores para letras maiúsculas.

Valores ausentes são preenchidos utilizando a moda da coluna.

## Análises realizadas

### Produção por estado

São identificados os estados que apresentam a maior produção anual de:

* Etanol hidratado;
* Etanol anidro.

A análise é realizada agrupando os dados por **ano e estado**.

### Produção por região

É analisada a evolução da produção de etanol nas diferentes regiões brasileiras ao longo dos anos.

Os resultados são apresentados em gráficos de linha para facilitar a comparação entre as regiões.

### Variação da produção de etanol hidratado

É analisada a variação da produção de etanol hidratado entre os estados durante o período estudado.

A diferença entre o maior e o menor valor anual de cada estado é utilizada para identificar aqueles que apresentaram maior variação de produção.

### Estados abaixo da média considerando o desvio padrão

Para cada ano, é calculada a média e o desvio padrão da produção de etanol anidro entre os estados.

É utilizado como referência o limite:

```text
Limite inferior = Média - Desvio Padrão
```

Estados com produção abaixo desse limite são identificados e apresentados graficamente.

## Principais resultados

A análise permite observar uma forte concentração da produção de etanol em determinados estados brasileiros.

Entre os estados que se destacam na produção estão **Mato Grosso, Mato Grosso do Sul, Goiás, São Paulo, Minas Gerais e Paraná**, especialmente na produção de etanol hidratado.

Também é possível observar que as regiões **Sudeste e Centro-Oeste** apresentam os maiores volumes de produção durante o período analisado.

A análise da variação da produção de etanol hidratado indica diferenças relevantes entre os estados ao longo dos anos.

## Visualizações

O projeto utiliza gráficos de:

* Barras para comparação da produção entre estados;
* Linhas para evolução temporal da produção por região;
* Barras para análise da variação da produção por estado;
* Barras para identificação de estados abaixo do limite definido pela média e desvio padrão.

## Estrutura do projeto

```text
├── dados/
│   └── ap2-combustivel-producao.csv
│
├── analise.py
│
└── README.md
```

## Como executar

### 1. Clone o repositório

```bash
git clone URL_DO_SEU_REPOSITORIO
```

### 2. Instale as dependências

```bash
pip install pandas numpy matplotlib seaborn
```

### 3. Execute o código

```bash
python analise.py
```

O código também pode ser executado diretamente no **Google Colab**, realizando a instalação/importação das bibliotecas necessárias e executando as células do notebook.

## Bibliotecas

O projeto utiliza as seguintes bibliotecas:

```python
import pandas as pd
import numpy as np
import unicodedata
import re
import seaborn as sns
import matplotlib.pyplot as plt
```

## Observação

As conclusões apresentadas são baseadas exclusivamente nos dados disponíveis no dataset e nas técnicas de tratamento e análise utilizadas no projeto. Portanto, possíveis variações observadas na produção não devem ser atribuídas automaticamente a fatores externos sem uma análise adicional dessas variáveis.

## Autor

**Bruno Henrique Pacheco Prudêncio**

Projeto acadêmico desenvolvido para estudo de **Ciência de Dados, limpeza de dados e análise exploratória**.

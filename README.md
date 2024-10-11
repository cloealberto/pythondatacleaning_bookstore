# 📊 Manipulando Colunas de um DataFrame com Pandas

Este repositório documenta como remover colunas desnecessárias de um DataFrame usando o Pandas em Python. Vamos abordar como otimizar um DataFrame ao remover informações irrelevantes para uma análise específica. 📊

## 🚀 Introdução

Muitas vezes, você encontrará dados que não são úteis para sua análise. Imagine que você tenha um dataset com informações de alunos (nome, nota, endereço, nomes dos pais), mas você quer focar apenas nas notas. Nesse caso, colunas como "endereço" e "nomes dos pais" não são necessárias e podem ser removidas para melhorar a performance.

O Pandas nos oferece uma maneira simples de remover colunas indesejadas usando a função `drop()`. Vamos ver como fazer isso! 🧑‍💻

## 📦 Carregando o Dataset

Primeiro, vamos carregar um dataset de exemplo a partir de um arquivo CSV: `import pandas as pd` `df = pd.read_csv('books_dataset.csv')` `df.head()`

## ✂️ Removendo Colunas Indesejadas

Identificamos as colunas que não são necessárias para a nossa análise: `deletar_colunas = ['Edition Statement', 'Corporate Author', 'Corporate Contributors', 'Former owner', 'Engraver', 'Contributors', 'Issuance type', 'Shelfmarks']` `df.drop(deletar_colunas, inplace=True, axis=1)`

Aqui, estamos passando a lista `deletar_colunas` com os nomes das colunas que queremos remover e usando `inplace=True` para que as mudanças sejam feitas diretamente no DataFrame.

## 🔄 Mudando o Índice

Podemos definir uma coluna como índice do DataFrame para melhorar a legibilidade e eficiência das consultas. Vamos usar a coluna `Identifier` como índice: `df.set_index('Identifier', inplace=True)` `df.head()`

Agora, o DataFrame está indexado pela coluna `Identifier`. Isso torna mais fácil acessar registros específicos, como: `df.loc[206]`

## 🧹 Limpando os Dados

É importante padronizar os dados para garantir a consistência. Vamos começar com a coluna `Date of Publication` (Data de Publicação). Podemos usar expressões regulares para extrair apenas o ano:<br> `regularexpression = r'^(\d{4})'` <br>`extrair_ano = df['Date of Publication'].str.extract(regularexpression, expand=False)` <br>`df['Date of Publication'] = pd.to_numeric(extrair_ano)`

Isso transformará as datas em valores numéricos, permitindo cálculos futuros! 📅

## 🌍 Limpando a Coluna de Local de Publicação

Usamos `np.where` para substituir valores inconsistentes na coluna `Place of Publication` (Local de Publicação), combinando o poder de Pandas com a função condicional `np.where`: `import numpy as np` <br>`lugar_publicacao = df['Place of Publication']` <br>`londres = lugar_publicacao.str.contains('London')` <br>`oxford = lugar_publicacao.str.contains('Oxford')` <br>`df['Place of Publication'] = np.where(londres, 'London', np.where(oxford, 'Oxford', lugar_publicacao.str.replace('-', ' ')))`

Agora os valores estão limpos e padronizados! ✨

## 💡 Dicas Técnicas

- A função `drop()` pode ser usada para remover tanto linhas quanto colunas.
- Para melhorar a eficiência, podemos passar as colunas a serem mantidas diretamente ao carregar o DataFrame com `usecols` no `pd.read_csv()`.

## 🔧 Tecnologias Utilizadas

- Python 🐍
- Pandas 📊
- NumPy 🔢

## 📖 Leitura Adicional

- [Documentação do Pandas](https://pandas.pydata.org/)
- [Regular Expressions: Regexes in Python](https://docs.python.org/3/library/re.html)



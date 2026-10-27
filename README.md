# Análise de Recursos Humanos com SQL e Python

**Disciplina:** Visualização de Dados e Business Intelligence — Módulo 1 (Projeto de Recuperação)  
**Aluno(a):** [Franciny Lieny Souza]  
**Turma:** [Curso de BI]

## Objetivo

Investigar a distribuição de funcionários por departamento, cargo, cidade, país e região, além de comparar salários atuais entre grupos e anos de admissão, utilizando o esquema HR do FreeSQL, consultas SQL e análise exploratória em Python.

## Fonte de dados e consultas

Fonte: [FreeSQL](https://freesql.com/), esquema **HR**. Tabelas: `EMPLOYEES`, `DEPARTMENTS`, `JOBS`, `LOCATIONS`, `COUNTRIES` e `REGIONS`.

1. **Query 1:** funcionários, departamentos, cargos e salários; dois `LEFT JOIN` e filtro `SALARY > 0`.
2. **Query 2:** funcionários por cidade, país e região; quatro `LEFT JOIN` e filtro de departamento não nulo.
3. **Query 3:** data e ano de admissão, salário atual, departamento e cargo; dois `LEFT JOIN`, `EXTRACT`, `WHERE` e `ORDER BY`.

As consultas de referência estão em `consultas.sql`. **Antes da entrega, confira se correspondem exatamente às consultas executadas no FreeSQL.** Os CSVs originais `query_01.csv`, `query_02.csv` e `query_03.csv` precisam ser adicionados à pasta `dados/`.

## Metodologia

Os dados são importados em Python com Pandas. Foram padronizados nomes de colunas, removidas linhas inteiramente vazias e duplicatas, convertidos salários para valores numéricos e datas para formato de data. A análise calcula média, mediana, mínimo, máximo e desvio padrão; compara salários por departamento e cargo; conta funcionários por localidade; agrupa anos de admissão e cruza esses anos com departamentos. Outliers salariais são identificados pelo método IQR (1,5 × intervalo interquartil). Os gráficos são gerados com Matplotlib e Seaborn.

## Resultados principais

- **107 funcionários** nas análises salariais e por ano de admissão; **106** na distribuição geográfica devido ao filtro de departamento.
- Salário médio geral: **6.461,83**; mediana: **6.200,00**; mínimo: **2.100,00**; máximo: **24.000,00**; desvio padrão: **3.909,58**. Valores na unidade monetária da base, sem moeda explicitada.
- O departamento **Executive** apresenta a maior média salarial (**19.333,33**, 3 funcionários). **Shipping** possui o maior quadro (**45 funcionários**) e média salarial de **3.475,56**.
- O cargo **President** apresenta o maior salário (**24.000,00**, um funcionário).
- Distribuição por país: Estados Unidos (**68**), Reino Unido (**35**), Canadá (**2**) e Alemanha (**1**).
- O maior grupo por ano de admissão é **2015 (29 funcionários)**, seguido de **2016 (24)** e **2017 (19)**. Juntos, são **72 funcionários (67,3% da base)**.
- Salários médios atuais dos admitidos em **2015: 6.824,14**; em **2016: 5.045,83**.
- Método IQR: Q1 = **3.100,00**, Q3 = **8.900,00**, IQR = **5.800,00**, limite superior = **17.600,00**; **um outlier**: salário de **24.000,00** do cargo President.

## Interpretação e limitações

A remuneração varia significativamente entre departamentos e cargos. Médias de grupos muito pequenos devem ser interpretadas com cautela. O salário de 24.000,00 é estatisticamente atípico, mas pode ser compatível com a função de presidência; portanto, não foi excluído. A consulta geográfica exclui um funcionário sem departamento associado. As comparações por ano de admissão refletem **salários atuais de grupos admitidos em anos diferentes**, não salários iniciais nem evolução salarial. A base não representa necessariamente todas as admissões históricas da empresa.

## Estrutura e execução

- `consultas.sql`: consultas SQL de referência.
- `dados/`: adicionar os três CSVs originais exportados do FreeSQL.
- `analise_rh_bi.ipynb`: notebook executado no Google Colab.
- `analise_rh.py`: versão do código em Python, destinada à execução no Colab (utiliza `google.colab.files`).
- `resultados/`: tabelas de estatísticas e agrupamentos exportadas.
- `graficos/`: quatro visualizações produzidas pela análise.

Para reproduzir: (1) executar as consultas no FreeSQL; (2) salvar os resultados como `query_01.csv`, `query_02.csv` e `query_03.csv`; (3) abrir o notebook no Google Colab; (4) executar a célula e selecionar os três CSVs; (5) conferir tabelas, gráficos e arquivo ZIP exportado. Bibliotecas: `pandas`, `numpy`, `matplotlib`, `seaborn` e `google.colab`.

## Melhorias futuras

Validar as datas com formato explícito; preservar um relatório de duplicações antes da remoção; comparar remuneração por nível de cargo e departamento; avaliar distribuições por região e faixa salarial com tamanhos amostrais mínimos; documentar o efeito dos filtros SQL.

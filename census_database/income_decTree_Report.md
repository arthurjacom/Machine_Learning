# Relatório Árvore de Decisões Census Adult Income
## Relatório dos resultados obtidos com a aplicação do algoritmo árvore de decisões a base census adult income 

### Objetivo
Iremos criar um algoritmo preditivo para classificar quais indivíduos recebem mais ou menos que 50 mil por ano com os dados fornecidos na base de dados criada em 1996 pela United States Census Bureau (USCB), a principal agência do sistema de estatística federal dos EUA.

### Obtenção dos dados
A base de dados está disponível para download gratuito no site [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/census+income).

### Pré-processamento

Todos os dados do tipo object foram transformados em dados numéricos por meio da biblioteca sklearn preprocessing, onde cada valor dentro de uma coluna foi substituído por um número em ordem crescente e alfabética, começando sempre pelo 0 até a quantidade máxima de valores diferentes presentes na coluna.

As colunas education e marital.status foram excluídas pois as colunas relationship e education.num possuem informações parecidas, native.country e fnlwgt também foram exluidas porque suas informações são irrelevantes ao projeto.

Durante a exploração da base, verifiquei que existiam missing values (Valores faltantes) preenchidos com ‘?’ (interrogação) que após o pré-processamento foram substituídos por ‘0’ (zero) nas colunas workclass e occupation. 
Esses valores correspondem a pouco mais de 2 mil e 400 linhas de dados que não valem a pena serem excluídos, por isso eu substitui os missing values pelo valor mais frequente 

* Em workclass o valor mais frequente é 4 = Private;
* Em occupation o valor mais frequente é 10 = Prof-specialty.

Por último renomeamos algumas colunas apenas para facilitar a leitura dos dados, substituindo ‘.’(ponto) por ‘_’(underline) e trocando ‘education_num’ por ‘education’.

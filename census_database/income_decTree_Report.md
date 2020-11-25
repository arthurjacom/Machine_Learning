# Relatório Árvore de Decisões Census Adult Income
### Relatório dos resultados obtidos com a aplicação do algoritmo árvore de decisões a base census adult income 

## Objetivo
Iremos criar um algoritmo preditivo para classificar quais indivíduos recebiam mais ou menos que 50 mil dolares por ano com os dados fornecidos na base de dados **Census**, criada em 1996 pela *United States Census Bureau (USCB)*, a principal agência do sistema de estatística federal dos EUA.

## Obtenção dos dados
A base de dados está disponível para download gratuito no site [*UCI Machine Learning Repository*](https://archive.ics.uci.edu/ml/datasets/census+income).

## Pré-processamento

Todos os dados do tipo *object* foram transformados em dados numéricos por meio da biblioteca *sklearn preprocessing*, onde cada valor dentro de uma coluna foi substituído por um número em ordem crescente e alfabética, começando pelo 0 até a quantidade máxima de valores diferentes presentes na coluna.

As colunas *education* e *marital.status* foram excluídas pois as colunas *relationship* e *education.num* possuem informações parecidas, *native.country* e *fnlwgt* também foram deletadas porque suas informações são irrelevantes ao projeto.

Durante a exploração da base, verifiquei que existiam *missing values* preenchidos com ponto de interrogação ('?') que após o pré-processamento foram substituídos por zeros('0') nas colunas workclass e occupation. 
Esses valores correspondem a pouco mais de 2 mil e 400 linhas (cerca de 7% do volume da base de dados) que não valem a pena serem excluídos, por isso eu substitui os missing values pelos valores mais frequentes em cada coluna.

* Em *workclass* o valor mais frequente é 4 = *Private*;
* Em *occupation* o valor mais frequente é 10 = *Prof-specialty*.

Por último renomeamos algumas colunas apenas para facilitar a leitura dos dados, substituindo ponto '.' por *underline* ‘_’ e trocando *‘education_num’* por *‘education’*.

## Testes

Durante os testes eu queria evitar ter uma acurácia alta e um árvore gigantesca ou uma árvore pequena e uma acurácia baixa, então o objetivo era encontrar um equilibrio entre os dois, mas se eu tivesse que sacrificar um pelo outro, escolheria ter uma árvore um pouco maior por mais acurácia.

1. **teste.size** e **random.state**: Realizei alguns testes com *test.size* usando valores de 10% a 40% e com *random.state* de 50 a 300, alguns resultados apresentaram mudanças positivas e outros negativos, mas a melhor combinação foi a combinação inicial com *test.size* em 0.30 e o *random.state* em 100.

2. **max_depth**: Após a realização de diversos testes com valores diferentes cheguei a conclusão que o melhor valor de profundidade vária de **6 a 8**, valores menores que 6 diminuem a acurácia enquanto valores iguais ou maiores que 10 criam uma árvore muito maior com pouco aumento na taxa de acertos. 
* Curiosamente a profundidade 9 sempre apresentava uma queda de acurácia se assemelhando aos valores inferiores a 5 ainda que a árvore de decisões seja muito maior. 
* A profundidade no 10 com *splitter best* foi a combinação que apresentou a maior acurácia registrada em 86.1%.
 
3. **splitter**: Entre as configurações de *splitter best* e *random*, o *best* apresentou uma melhora de 0.1% na acurácia em grande parte dos testes, apesar de ser uma mudança insignificativa eu escolhi manter o *splitter best*.

4. **min_samples_split** e **min_samples_leaf**: Esses dois atributos limitam o valor minimo para criação de um novo nódulo e de uma nova "folha" da árvore, eles estão diretamente ligados ao tamanho da árvore de decisões e quanto maior eles são, mais eles diminuem a acurácia, por isso é muito dificil equilibrá-los.
Após realizar diversos testes, qualquer valor acima de 300 deixava a acurácia abaixo de 85%, então eu reduzi o valor de 5 em 5 até que ele sempre utilizasse no minimo 1% da base de dados e ao mesmo tempo não reduzisse a acurácia para abaixo de 85%, o valor ideal foi 215 para ambos os atributos.

## Resultado

 Finalizada a etapa de testes, eu escolhi um modelo final pensando em 3 aspectos: 1. Acurácia; 2. Tamanho da Árvore de Decisões e 3. Qualidade das Classificações.
 A acurácia é a métrica calculara para medir a qualidade do modelo, o tamanho da árvore de decisões não podia ser exageradamente grande pois existiram dezenas de nódulos repetidos, e a qualidade das classificações é impedir que o modelo use quantidades muito baixas de amostras para fazer uma classificação que provavelmente estara errada porque é baseada em menos de 0.5% dos dados. Seguindo essas diretrizes, esse foi o meu resultado: 

#### Confusion Matrix

* (0) <50k: 87% de Acertos e 13% de Erros.
* (1) >50k: 78% de Acertos e 22% de Erros.

#### Classification Report

* Precision: (0) 87% - (1) 78%
* Recall: (0) 95% - (1) 54%
* F1-socre: (0) 91% - (1) 64%
* **Acurácia**: 85.34%

## Obrigado!

 Obrigado por ter se interessado no meu trabalho! 
 Se quiser conversar comigo sobre esse ou qualquer um dos meus trabalhos você pode me encontrar no [Linkedin](https://www.linkedin.com/in/arthur-jacom/), no [Github](https://github.com/arthurjacom) ou no [Kaggle](https://www.kaggle.com/arthurjacom)!

# Classificação de Saúde Fetal com AutoML

<p align="center">
  <img src="capa_p6.png" >
</p>

## Contexto

A mortalidade de bebês durante o período de gestação é um problema que exige coordenação de diversas áreas, não somente da saúde. Desde a assistência social, infraestrutura de transporte, até o desenvolvimento de tecnologias e metodologias para **identificação, prevenção e tratamento das complicações que ocorrem durante a gravidez**.

O óbito fetal é um problema sério que tem, além da perda da vida do bebê, consequências diretas na saúde da mãe, devido ao trauma e aos riscos inerentes à condição da morte do bebê. A **mortalidade maternal** é também uma grande preocupação, visto que cerca de **296 mil mortes ocorrem durante e após a gravidez, em dados de 2017 nos EUA**. Desse número, **cerca de 94% morrem por falta de recursos médicos e acompanhamento**. Trata-se, portanto, de um problema grave e que pode ser previnido com inteligência e bom gerenciamento de recursos.

No Brasil, a taxa de mortalidade maternal em 2021 era de 107 mortes a cada 100 mil nascimentos. Da mesma forma como nos EUA, a mortalidade maternal está associada à falta de recursos e acompanhamento médico recorrente, e à falha em reconhecer os sintomas que levam à perda do bebê.

De acordo com o panorama levantado nessas pesquisas, para reduzir as taxas de mortalidades fetal e maternal é necessário:

1. Reconhecer os problemas de saúde associados à mãe, doenças congênitas, condições hereditárias e complicações da gravidez, a tempo de se realizar um tratamento;

2. Providenciar acesso aos sistemas de saúde, melhorando a rede assistencial para mulheres grávidas, bem como a infraestrutura de transporte;

3. Conceder o diagnóstico e o tratamento apropriados, com acompanhamento médico frequente.

## Relevância

Este projeto se propõe a construir modelos de classificação da saúde fetal baseados em dados referentes à parâmetros que indicam a saúde do bebê. Para isso, utilizaremos dados do exame de **Cardiotocofragia** (CTG), que é um procedimento que utiliza pulsos de ultrassom para analisar a frequência cardíaca do bebê, o movimento fetal, contrações uterinas, entre outros indicadores.

Portanto, nossos objetivos consistem em responder três perguntas:

1. É possível utilizar o CTG para prever a saúde fetal?

2. Se sim, quais são os fatores que mais contribuem para essa previsão?

3. Quais abordagens podem ser tomadas por planos de saúde para poderem implementar e priorizar o reconhecimento desses fatores?

A abordagem do problema passará pela criação de modelos supervisionados de aprendizado de máquina, com a construção de pipelines para pré-processamento e ajuste dos dados, buscando minimizar a taxa de erros de falsos negativos, que corresponderiam a casos graves classificados como normais. Espera-se, com isso, ter como resultado um modelo de classificação confiável para auxiliar no diagnóstico de gravidez de risco, buscando salvar as duas vidas, da mãe e do bebê.

## Resultados

Foram utilizadas duas abordagens: a primeira consistiu na construção de um pipeline para pré-processamento e ajuste dos modelos, com a utilização de técnicas como a busca em grade com validação cruzada (*GridSearchCV*) e análise de desempenho através da curva de *precisão-recall*. Foram testados os modelos de **regressão logística**, **random forest**, **SVM** e **Extra Trees Classifier**, buscando minimizar a taxa de falsos negativos. O melhor desempenho, com maior *recall*, foi do modelo de **Extra Trees**, que alcançou uma taxa de falsos negativos de aproximadamente 3% em dados nunca antes vistos.

A segunda abordagem consistiu na aplicação de *machine learning* automatizado através da biblioteca **PyCaret**. Neste caso, buscou-se configurar o pipeline automatizado para o balanceamento e normalização dos dados, resultando na construção de diversos classificadores e posterior comparação entre eles. Foi escolhido aquele que obteve o maior *recall*, que no caso foi o algoritmo de Análise de Discriminante Linear, ou *Linear Discriminant Analysis*. Na validação, o modelo otimizado atingiu 97% de *recall*, enquanto que nos testes de desempenho com dados nunca antes vistos, obteve um *recall* de aproximadamente 94%. 

Comparando-se as duas abordagens, nota-se que os pipelines que geraram os dois modelos foram distintos, além também da maneira como se trataram os dados durante o pré-processamento. Ambas as abordagens resultaram em ótimos resultados para a classificação da saúde fetal, havendo porém a prevalência do modelo de **Extra Trees** sobre o **LDA** para dados novos do conjunto de teste.

|      **Modelos**      | **Recall** | **AUC** | **Acurácia** |
|:---------------------:|:----------:|:-------:|:------------:|
| _Regressão Logística_ | 0.95       | 0.84    | 0.77         |
| _Random Forest_       | 0.92       | 0.93    | 0.94         |
| _SVM_                 | 0.94       | 0.91    | 0.89         |
| _Extra Trees_         | 0.97       | 0.92    | 0.90         |
| _LDA_                 | 0.94       | 0.95    | 0.83         |

## Conclusões

O projeto como um todo ajudou a clarificar pontos importantes de atenção para o diagnóstico da saúde fetal que podem ser usados por médicos obstetras e neonatologistas. Alguns atributos do exame de CTG foram destacados como sendo informativos para a previsão de casos graves, como **aceleração e movimentos do bebê**, **contrações uterinas**, **variações anormais de curto e longo prazo** e **desacelerações severas**.

Além disso, a recomendação é que o exame de CTG seja feito o mais frequente possível durante o período de gestação, principalmente por sua simplicidade e facilidade de interpretação. Os exames de CTG são capazes de prever a saúde fetal e reduzir a mortalidade tanto materna quanto do bebê, tornando-se uma opção de custo efetivo baixo para evitar fatalidades.

Da parte de inteligência de dados, modelos de classificação como o **Extra Trees** fornecem uma boa capacidade preditiva e um nível de personalização que permite identificar casos suspeitos ou patológicos com o mesmo nível de precisão, para que o tratamento comece o mais rápido possível. É recomendada uma abordagem que diminua o limiar para a classe positiva, visando que, ao menor sinal de suspeita de risco, os pacientes sejam checados.

## Próximos Passos

O CTG é um exame bem difundido para a análise da saúde fetal, de modo que mais dados de exames melhorariam a performance dos modelos de classificação. Com mais dados, podemos **testar a robustez do modelo em identificar tendências nas variáveis**, buscando sempre **diminuir os erros de falsos negativos** para nenhum caso de risco fique sem tratamento. Pode-se trabalhar na construção de mais atributos para o CTG, trabalhando em colaboração com médicos e ouvindo as queixas e sintomas das mães. 

Por fim, apesar de termos explorado bem os efeitos dos batimentos cardíacos e taxas de aceleração na saúde fetal, não foram explorados as medidas de histograma do exame, nem o que significam seus valores no contexto da previsão de problemas para o bebê.

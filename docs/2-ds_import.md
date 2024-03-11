# Ciência de Dados e Importação {#ds-import}

:::{.warn}
este capítulo está em construção. O que segue abaixo é apenas um rascunho.
:::

Neste capítulo, descreverei os fundamentos e etapas de um projeto de ciência de dados. Também adianto como importar diferentes tipos de arquivos para o R usando o pacote "readr".

## Ciência de Dados

### Introdução

**Ciência de Dados:** "a aplicação de métodos estatísticos e computacionais para a análise de dados".

Um projeto de ciência de dados normalmente segue o seguinte fluxo:

<!--
\begin{figure}
\centering
\includegraphics[width=0.9\textwidth, keepaspectratio]{../Aula_ii1/data-science-explore.png}
\caption*{Fonte: [R for Data Science, seção 1](https://r4ds.had.co.nz/introduction.html]}
\end{figure}
-->

### Preparar

- **Importar os dados:** o passo inicial de qualquer projeto de ciência de dados. É necessário saber o tipo de arquivo, o tipo da fonte (arquivos, _databases_, _API_'s), e as ferramentas de importação disponíveis.

- **Arrumar (tidy) os dados:** limpar e organizar os dados de acordo com o formato necessário. Em D.S., muitas vezes queremos o formato "tidy", onde cada coluna representa uma variável e cada linha uma observação. 

- **Transformar os dados:** refinar seus dados para facilitar a uma visualização ou modelagem específica. Este passo envolve reduzir observações, criar novas variáveis e calcular estatísticas resumo.

Esses três passo juntos são referidos como _data wrangling_ ("preparação" de dados).


### Entender e Explorar

- **Visualização:** explorar os dados de maneiras mais interessantes visualmente. Boas visualizações podem revelar mais informação sobre o problema, levantar questões para se atentar, e demandas por mais dados e/ou outros modelos.

- **Modelagem:** modelos são ferramentas para responder perguntas sobre o processo gerador dos dados. Eles são conjuntos de hipóteses sobre o problema em mãos, acompanhados por um método computacional para sua estimação. Cada modelo tem seu conjunto de hipóteses, e seus métodos de estimação.

- **Transformar os dados:** após entender melhor as demandas do problema, é comum voltar ao passo de transformação dos dados, e repetir o ciclo, até que toda a informação quista seja obtida.


### Communicating and Executing

- **Comunicação:** após o problema ser analisado, é preciso reportar os resultados 

- **Communication:** Communication is integral to any data analysis project. It involves conveying your findings to others effectively. No matter how insightful your models or visualizations are, their value is limited if you cannot communicate results in a clear and understandable manner.

- **Programming:** Programming is a pervasive tool in data science. While not mandatory to be an expert programmer, improving programming skills aids in automating tasks and tackling new challenges efficiently. Programming is a cross-cutting skill used throughout the entire data science project.



<div class="double-hrule"></div>

## Complemento {.unlisted .unnumbered}

### Recapitulando {-}


---

### Exercícios {-}


---

### Dicionário de Funções {-}


---

### Referências {-}


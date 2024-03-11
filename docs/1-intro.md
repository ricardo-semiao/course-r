

# Parte I - R Base {#intro1 .unnumbered}

Bem vindo à primeira parte deste livro, onde estudaremos os conceitos na base do R. Partirei do zero absoluto, de modo que é possível que o leitor tenha algum nível de familiaridade com os temas, mas provavelmente, não na profundidade aqui abordada.

Nessa parte mais "teórica", é difícil de traçar o limite no nível de complexidade ideal. Por conta disso, muitos conceitos tiveram de ser introduzidos rapidamente. Mas não se assuste, muitas vezes, meu objetivo maior é passar uma intuição geral de como o R funciona, e dar um primeiro contato com os temas mais complexos. Tento ao máximo deixar claro onde gastar seu cérebro e onde nem tanto.

Meu foco é mostrar a lógica do R, a "sintaxe e semântica" da linguagem. A "gramática/vocabulário", isto é, funções, truques, e aplicações específicas, serão ensinadas de passagem e via exercícios. Mas no final, a ideia é ter apresentado a maioria das funções comumente relevantes, construindo uma lista de referência para futuras consultas.

Os capítulos dessa seção estão organizados da seguinte maneira:

- Capítulo \@ref(syntax-vars): aqui aprenderemos o básico sobre a sintaxe do R. Como imputar números e texto, o que são expressões e variáveis, e como realizar operações básicas. No geral, um capítulo bastante simples.
- Capítulo \@ref(data-attrs): a organização de tipos de dados no R é elegantemente simples, incluindo complexidade através da existência de metadados. A principal conclusão será entender a relação entre os diferentes tipos, porque esse conhecimento torna mais fácil pensar como uma mesma operação é aplicada em cada tipo de dado.
- Capítulo \@ref(subset): nessa altura do campeonato, capaz que você esteja cansado de ver apenas teoria, esse capítulo é o mais "gramatical" de todos. Aprenderemos o que é a operação de selecionar e alterar partes de uma variável. Aqui, já fica claro o benefício de entender a organização dos tipos de dados.
- Capítulo \@ref(control-conds): aprenderemos a controlar o fluxo de um programa, isto é, como fazer um programa tomar decisões e repetir operações. Aprenderemos também a lidar com erros e avisos.
- Capítulo \@ref(funs-envs): em oposição ao capítulo 3, agora é hora de dar atenção aos sentimentos do R. Estávamos utilizando-as, mas não explicamos o que são as funções. Esse é o capítulo mais desafiador, mas boa parte da dificuldade pode ser deixada de lado, com perdas reduzidas ao leitor.
- Capítulo \@ref(paradigms): aqui, aprenderemos sobre os paradigmas/estilos de programação funcional, orientada ao objeto, e meta, especificamente sobre sua abordagem no R. A programação funcional é uma ferramenta com ligação direta nos projetos de ciência de dados; Entender o básico de POO no R é importante para entender o uso de funções[^Se chutou "objetos", chutou errado.]; Metaprogramação é um assunto útil em si mesmo, mas especialmente importante para entender as bases do tidyverse na segunda parte do livro.
- Capítulo \@ref(others1): por fim, temos algum outros tópicos úteis, mas não essenciais para o seguimento do livro. Aqui, aprenderemos sobre algumas ferramentas de melhoria de vida que o RStudio provê, e alguns temas avançados sobre gerenciamento de memória, performance, e organização.
- Recapitulado: não só em cada capítulo, mas cada parte deste livro, existe uma seção para retomar os conteúdos, especialmente o que será mais útil para a próxima parte.

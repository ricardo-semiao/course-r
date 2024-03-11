

# Subsetting {#subset}

:::{.warn}
este capítulo está em construção. O que segue abaixo é apenas um rascunho.
:::


## Introdução

Falamos sobre vetores, agora falaremos sobre como selecionar/alterar seus elementos\medskip

Existem três operadores, `[`, `[[`. e `$`. Começaremos com `[`\medskip

A sintaxe geral é `x[...]`{.r}, podemos usar várias técnicas diferentes no lugar de "..."\medskip\pause

Para os exemplos: 

```r
x <- c(1.3, 7.4, 6.0, 5.9)
m <- matrix(1:9, nrow = 3, ncol = 3)
colnames(m) <- c("A", "B", "C")
df <- as.data.frame(m)
l <- list("a" = 1:3, "b" = "oi", "c" = 4:6)
```


## Operador [

\framesubtitle{Com vetores}

Existem seis maneiras: 

- **Inteiros positivos:** retornam elementos nas posições
  - `x[1] #> 1.3`{.r}
  - `x[1:3] #> 1.3 7.4 6.0`{.r}
  - `x[c(1,3)] #> 1.3 6.0`{.r}
  - Obs1: índices decimais são truncados: `x[1.7] == x[1]`{.r}
  - Obs2: factors são tratados como integers\pause
- **Inteiros negativos:** retornam todos os elementos menos os das posições
  - `x[-c(1,3)] #> 7.4 5.9`{.r}

\framesubtitle{Com vetores}
- **Vetores lógicos:** retornam os elementos nas posições onde tem-se `TRUE`{.r}'s
  - `x[c(TRUE, TRUE, FALSE, FALSE)] #> 1.3 7.4`{.r}
  - O vetor lógico deve ser do mesmo tamanho. O R tenta corrigir transgressões, mas as regras de "reciclagem" são confusas (`x[c(TRUE, FALSE)]`{.r})\pause
- **Vetores de texto:** retornam os elementos com os nomes escolhidos
  - `c(a = 1, b = 2, c = 3)[c("a", "c")] #> 1 3`{.r}\pause
- **Nada:** `x[]`{.r} retorna o vetor original
- **Zero:** retorna um vetor de tamanho 0

Obs: todos esses métodos podem reordenar os elementos `x[c(1, 3, 2)]`{.r}


\framesubtitle{Com matrizes e arrays}

Com matrizes (vetores com dimensão), existem três maneiras:

- **Múltiplos vetores:** um vetor para cada dimensão
  - `m[c(TRUE, FALSE, TRUE), c("B", "A")]`{.r}
  - Um vetor omisso retorna todos os "elementos da dimensão": `a[, c(1, 3)]`{.r}
  - Para arrays, use um argumento para cada dimensão `a[1:2, 2, , 4]`{.r}\pause
- **Vetor único:** como matrizes são vetores, podemos tratá-las como tal
  - `m[5:7]`{.r} do elemento 5 até o 7 (a ordem é "column-major")
  - Podemos usar uma matriz lógica aqui, similar à usar um vetor lógico\pause
- **Matrizes seletoras:** onde cada coluna é uma dimensão, e cada linha um elemento quisto
  - `m[rbind(c(1,1), c(3,1), c(2,4))]`{.r}
  - Para arrays, precisamos de três ou mais colunas


\framesubtitle{Com listas}

**Listas:** mesmas maneiras que com vetores atômicos. `[` sempre retorna uma lista, mesmo ao selecionar um único elemento

::: {.example}
E para data frames? O que `df[1:2]`{.r} deve retornar? E `df[1:2, ]`{.r}? É "natural" que esses métodos coexistam?
:::


\framesubtitle{`drop = TRUE`}
O operador `[` simplifica a dimensão do resultado

- Em matrizes/arrays, dimensões de _length_ 1 são desfeitas
  - `m[1,]`{.r}, e `m[,1]`{.r}
  - Com vetores únicos, todas são: `m[1:9]`{.r}
- Data frames no "modo matriz" sofrem o mesmo, mas apenas para colunas
  - `df[1,]`{.r}
  - Mas `df[,1]`{.r} e `df[1]`{.r} mantêm a dimensão\pause

Isso é controlado pelo argumento `drop = TRUE` do operador\footnote[frame]{Causa comum de erros}. Podemos alterá-lo: `df[1, , drop = FALSE]`{.r}\medskip

Tibbles tem `drop = FALSE` por padrão, sempre retornando outra tibble/nunca simplificando (alá a preguiça)


## Operador [[ e $

Para selecionar um único elemento, podemos usar os operadores `[[` ou `$`\medskip

Para pegar um elemento, e não uma lista, precisamos usar `l[["a"]]`{.r} no lugar de `l["a"]`{.r}

::: {.example}
Porque não existe essa diferenciação para vetores atômicos (`x[1] == x[[1]]`{.r})? Pode ser útil usar `[[` mesmo assim?
:::
\pause

`l$a`{.r} é uma abreviação de `l[["a"]]`{.r}. Diferença: `$` faz "matching parcial" (da esquerda pra direita)\footnote[frame]{Vide a opção global `warnPartialMatchDollar`}. Duvido vocês adivinharem se tibbles fazem isso ou não


O operador [[ reage de maneiras estranhas quando se pede um elemento que não existe, as vezes retorna erro, as vezes `NULL`{.r}. Para lidar com isso, foram criadas as funções:

- `purrr::pluck()` sempre retorna NULL (ou um valor definido pelo usuário)
- `purrr::chuck()` sempre retorna um erro

Obs: existem também `@` e `slot()`{.r}, similares a `$` e `[[` que servem para objetos S4 e não serão tratados aqui


## Atribuição

Todos os operadores podem ser combinados com `<-`, numa operação chamada de sub-atribuição\medskip

O formato geral é `x[i] <- valor`{.r}. Alguns comentários:

- Cheque se `length(x[i]) == length(valor)`{.r}. Pode gerar erros ou resultados inesperados via reciclagem
- Podemos re-assinalar mais de um elemento por vez\pause
- Com listas, lembre que `l[i]`{.r} sempre é uma lista
  - `l[i] <- list(valor)`{.r} é similar à `l[[i]] <- valor`{.r}
  - `l[[i]] <- NULL`{.r} remove o item da lista, enquanto `l[i] <- list(NULL)`{.r} altera o item para `NULL`{.r}
- Podemos "alterar o conteúdo de um objeto" (mantendo sua estrutura) no lugar de "alterar o objeto em si", usando o subset vazio
  - `df[] <- as.list(df)`{.r} versus `df <- as.list(df)`{.r}
  
  
## Aplicações

::: {.example}
#### Lookup vectors
Dado o vetor de abreviações abaixo, como criar o vetor extenso ("male" e "female")
\vspace{-1em}

```r
x <- c("m", "f", "u", "f", "f", "m", "m")
```
\vspace{-1em}
\pause
**Resposta:**
\vspace{-1em}

```r
lookup <- c(m = "Male", f = "Female", u = NA)
lookup[x]
```
\vspace{-1em}
:::


::: {.example}
#### Lookup tables
Agora, queremos fazer o match de um vetor de "tipos" com a tabela que descreve cada tipo
\vspace{-1em}

```r
grades <- c(1, 2, 2, 3, 1)

info <- data.frame(grade = 3:1,
                   desc = c("Good", "Med.", "Poor"),
                   fail = c(F, F, T))
```
\pause
**Resposta:**
\vspace{-1em}

```r
info[match(grades, info$grade), ]
```
Para _merges_ mais complexos, usaremos as funções `merge()` e `dplyr::left_join()`
:::


::: {.example}
#### Amostragem aleatória
A função `sample(x, n)`{.r} escolhe n elementos aleatórios do vetor x. Como podemos utilizá-la para tirar uma amostra de um data frame?
\vspace{-1em}

```r
df <- data.frame(x = c(1, 2, 3, 1, 2),
                 y = 5:1,
                 z = letters[1:5])
```
\pause
**Resposta:**
\vspace{-1em}

```r
df[sample(nrow(df)), ]
df[sample(nrow(df), 3, replace = TRUE), ]
```
\vspace{-1em}
:::


::: {.example}
#### Expandindo linhas idênticas
É comum data frames terem uma coluna de "quantas vezes uma observação aparece". A função `rep(x, y)`{.r} repete cada entrada i do vetor `x` `y[i]`{.r} vezes. Como podemos usá-la para expandir linhas?
\vspace{-1em}

```r
df <- data.frame(x = c(2, 4, 1),
                 y = c(9, 11, 6),
                 n = c(3, 5, 1))
```
\pause
**Resposta:**
\vspace{-1em}

```r
df[rep(1:nrow(df), df$n), ]
```
\vspace{-1em}
:::


::: {.example}
#### Seleção negativa com characters
Com índices, podemos usar `-` para fazer seleção negativa. Para nomes, use a função `which()` e/ou `setdiff()`.
\pause
**Resposta:**
\vspace{-1em}

```r
df[setdiff(names(df), "n")]
df[which(names(df) !%in% c("a", "b"))]
```
\vspace{-1em}
:::


::: {.example}
#### Filtragem de datasets com condições
Como selecionar apenas as linhas do dataset `mtcars` cujo valor de "cyl" seja maior que 4?\medskip
\pause
**Resposta:**
\vspace{-1em}

```r
mtcars[mtcars$cyl > 4, ]
mtcars[mtcars$cyl > 4 & mtcars$gear == 5, ]
```
\vspace{-1em}
:::


  
<div class="double-hrule"></div>

## Complemento {.unlisted .unnumbered}

### Recapitulando {-}

\framesubtitle{Subsetting}
Vimos que existem seis maneiras básicas de acessar elementos de um vetor com `[`:

- **Inteiro positivo** com índices dos elementos quistos
- **Inteiro negativo** com índices dos elementos à ignorar
- **Vetor lógico** com `TRUE` nos índices dos elementos quistos
- **Vetor de texto** com os nomes dos elementos quistos
- **Nada**, `x[]`{.r}, retornando o vetor original
- **Zero**, retornando um vetor de tamanho 0

Adicionalmente, aprendemos sobre o comportamento de simplificação de dimensões (`drop = TRUE`)


\framesubtitle{Subsetting}
Sabendo as características dos tipos de dados (aula I.1) é fácil saber aplicar tais métodos aos diferentes objetos:

- Com matrizes, podemos:
  - Tratá-las como vetores (ordem "column-major")
    - Usar vetores atômicos ou até matrizes de mesmo tamanho
  - Tratar cada dimensão como uma seleção independente
    - Uso especial do método "Nada"
  - Usar matrizes seletoras
- Com listas, podemos:
  - Usar os mesmos métodos, retornando uma sub-lista
  - Usar `[[` e `$` para selecionar elementos específicos
- Com data frames, podemos tratá-los como matrizes ou listas, usando todos os métodos acima


\framesubtitle{Subsetting}
Estudamos também algumas aplicações

- Lookup vectors
- Lookup tables
- Resampling
- Ordenação
- Expansão de linhas agregadas
- Logical subsetting



---

### Exercícios {-}


---

### Dicionário de Funções {-}


---

### Referências {-}

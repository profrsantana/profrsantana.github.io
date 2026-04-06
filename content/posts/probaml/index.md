+++
date = '2026-04-06T09:08:56-03:00'
title = 'Probabilidade para Machine Learning'
series = ["Matemática para Machine Learning"]
tags = ["Probabilidade", "Machine Learning", "Matemática", "IA", "ML"]
+++

{{< katex >}}

Um dos tópicos que estou revisando esse ano é probabilidade, principalmente para aplicações em Machine Learning.

- [Probabilidade de um Evento](#probabilidade-de-um-evento)
- [Evento Complementar](#evento-complementar)
- [Resumo](#resumo)
- [Referências](#referências)


## Probabilidade de um Evento

De maneira simplificada, probabilidade é uma área da matemática que estuda a chance de eventos ocorrerem. Como em Machine Learning lidamos com dados e incertezas, a probabilidade é importante para entender como ler os resultados de modelos, e entender como metrifica-los.

Vou buscar escrever os notações matemáticas também, pois para os que estudam e trabalham com Machine Learning, é importante entender a notação para ler artigos científicos e livros da área.


Um exemplo simples de probabilidade é, partindo do suposto que tenho 10 alunos em uma sala e 3 deles conhecem futebol, qual a probabilidade de um aluno escolhido aleatoriamente jogar futebol? 

$$P(\text{futebol}) = \frac{\text{evento}}{\text{espaço amostral}} = \frac{\text{n alunos futebol}}{\text{n total alunos}} = \frac{3}{10} = 0,3$$

Então em um experimento aleatório, a probabilidade de escolher um aluno que joga futebol é 30%. Probabilidade sempre varia entre 0 e 1, ou 0 e 100%.

Vamos representar isso graficamente, usando o diagrama de Venn, que é uma representação visual de conjuntos e suas relações:

{{< mermaid >}}
graph TD
    subgraph Omega ["&Omega; - Espaço Amostral (10 Alunos)"]
        F(("Jogam Futebol: 
        30% - 3 Alunos"))
    end

    classDef omegaBox fill:#f4f9f4,stroke:#27ae60,stroke-width:2px,color:#27ae60,font-weight:bold
    classDef bola fill:#fff,stroke:#333,stroke-width:2px,color:#000,font-weight:bold
    class Omega omegaBox
    class F bola
{{< /mermaid >}}



Em notação matemática, ficaríamos assim:

_Espaço Amostral (pode-se usar a notação S ou Ω):_
$$n(\Omega) = 10$$

_Evento A (Alunos que jogam futebol):_
$$n(A) = 3$$

_Probabilidade:_
$$P(A) = \frac{n(A)}{n(\Omega)} = \frac{3}{10} = 0,3$$


## Evento Complementar 

O complementar de um evento é a probabilidade do evento não acontecer. Tendo em vista que nosso espaço amostral \(n(\Omega)\) possui todos os eventos possíveis, no nosso exemplo o numero de alunos, e que a probabilidade é sempre um valor entre 0 e 1, entao o resultado do evento complementar é 1 menos a probabilidade do evento acontecer.

\(P(A^c) = 1 - P(A)\)   tal que   \(A \cup A^c = \Omega\) 

No nosso exemplo, a probabilidade de escolher um aluno que não joga futebol é 70%:
$$P(\text{não futebol}) = 1 - P(\text{futebol}) = 1 - 0,3 = 0,7$$



## Resumo
Neste post, revisamos o conceito de probabilidade, que é a chance de eventos ocorrerem, e sua importância para Machine Learning. Usamos um exemplo simples de uma sala com 10 alunos, onde 3 jogam futebol, para calcular a probabilidade de escolher um aluno que joga futebol (30%) e o evento complementar (70%). Também representamos isso graficamente usando um diagrama de Venn. A probabilidade é fundamental para entender os resultados de modelos de Machine Learning e suas métricas.



## Referências

[Mathematics for Machine Learning and Data Science - deeplearning.ai](https://www.deeplearning.ai/courses/mathematics-for-machine-learning-and-data-science/)

[Probability and Statistics: The Science of Uncertainty - Michael J. Evans, Jeffrey S. Rosenthal](https://www.amazon.com/Probability-Statistics-Science-Uncertainty-Second/dp/1466575570)
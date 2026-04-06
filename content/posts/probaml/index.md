+++
date = '2026-04-06T09:08:56-03:00'
draft = true
title = 'Probabilidade para Machine Learning'
series = ["Matemática para Machine Learning"]
tags = ["Probabilidade", "Machine Learning", "Matemática", "IA"]
math = true
+++

{{< katex >}}

Um dos tópicos que estou revisando esse ano é probabilidade, principalmente para aplicações em Machine Learning.

De maneira simplificada, probabilidade é uma área da matemática que estuda a chance de eventos ocorrerem. Como em Machine Learning lidamos com dados e incertezas, a probabilidade é importante para entender como ler os resultados de modelos, e entender como metrifica-los.

Vou buscar escrever os notações matemáticos também, pois para os que estudam e trabalham com Machine Learning, é importante entender a notação para ler artigos científicos e livros da área.


Um exemplo simples de probabilidade é, partindo do suposto que tenho 10 alunos em uma sala e 3 deles conhecem futebol, qual a probabilidade de um aluno escolhido aleatoriamente jogar futebol? 

$$P(\text{futebol}) = \frac{\text{evento}}{\text{espaço amostral}} = \frac{\text{n alunos futebol}}{\text{n total alunos}} = \frac{3}{10} = 0,3$$

Então em um experimento aleatório, a probabilidade de escolher um aluno que joga futebol é 30%.

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

$$\text{Espaço Amostral: } n(\Omega) = 10$$
$$\text{Evento A: } n(A) = 3$$
$$\text{Probabilidade: } P(A) = \frac{n(A)}{n(\Omega)} = \frac{3}{10} = 0,3$$




## Referências

[Mathematics for Machine Learning and Data Science - deeplearning.ai](https://www.deeplearning.ai/courses/mathematics-for-machine-learning-and-data-science/)
+++
date = '2026-04-13T10:01:18-03:00'
title = 'Probabilidade para Machine Learning - Soma de Probabilidades e Probabilidade Condicional'
series = ["Matemática para Machine Learning"]
series_order = 2
tags = ["Probabilidade", "Machine Learning", "Matemática", "IA", "ML"]
+++
{{< katex >}}

Continuando a série de artigos sobre Probabilidade para Machine Learning, neste post vamos falar de soma de Probabilidades e Probabilidade Condicional, e os impactos disso para a construção de modelos de Machine Learning.


- [Soma das Probabilidades](#soma-das-probabilidades)
  - [Mutuamente Exclusivos](#mutuamente-exclusivos)
  - [Não Mutuamente exclusivos](#não-mutuamente-exclusivos)
    - [Independentes / Dependentes](#independentes--dependentes)
    - [Por que é importante entender a diferença entre eventos independentes e dependentes?](#por-que-é-importante-entender-a-diferença-entre-eventos-independentes-e-dependentes)
- [Probabilidade Condicional](#probabilidade-condicional)
- [Resumo](#resumo)
- [Referências](#referências)

## Soma das Probabilidades

Quando precisamos saber a probabilidade total de mais de um evento ocorrer, podemos usar a regra da soma de probabilidades, porem temos que levar em consideração se os eventos são mutuamente exclusivos ou independentes.

### Mutuamente Exclusivos
Eventos mutuamente exclusivos (em inglês Disjoint Events) são aqueles que não podem ocorrer ao mesmo tempo. Por exemplo, ao lançar um dado, <u>não é possível</u> obter um numero par e impar ao mesmo tempo, ou um exemplo mais voltado a aplicação de Machine learning, se eu tenho um modelo que classifica uma peça em "defeituosa" ou "não defeituosa", não é possível a peça ter as duas classificações ao mesmo tempo.

Matematicamente diríamos que \(P(A \cap B) = 0\), ou seja, a probabilidade de ambos os eventos ocorrerem ao mesmo tempo (interseção \(\cap\)) é zero.

Supomos que a probabilidade calculada pelo modelo seja de 0.4 para "defeito leve", e 0.5 para "defeito grave", 0.1 para "não defeituosa", e quero saber qual a probabilidade de uma peça ter defeito, ou seja de ter defeito leve <u>ou</u> defeito grave:

$$P(defeito) = P(\text{defeito leve}) + P(\text{defeito grave}) = 0.4 + 0.5 = 0.9 = 90\%$$
\(P(defeito)\) pode ser simbolizado também como a união (\(\cup\)) entre os eventos, ou seja, \(P(defeito) = P(\text{defeito leve} \cup \text{defeito grave})\).


### Não Mutuamente exclusivos

Eventos não mutuamente exclusivos são aqueles que podem ocorrer ao mesmo tempo. Por exemplo, supondo que você tem um modelo de detecção de objetos em uma imagem, e esse modelo detecta gatos e pássaros. É possível em que uma mesma imagem tenha um gato e um pássaro, ou seja, \(P(gato \cap pássaro) \) não é necessariamente zero.

Nesse caso, para calcular a probabilidade de um evento ou outro ocorrer, precisamos subtrair a probabilidade de ambos os eventos ocorrerem ao mesmo tempo, para evitar contar essa interseção duas vezes:
$$P(gato \cup pássaro) = P(gato) + P(pássaro) - P(gato \cap pássaro)$$

<svg width="400" height="250" xmlns="http://www.w3.org/2000/svg">
  <circle cx="150" cy="125" r="100" fill="rgba(52,152,219,0.3)" stroke="#3498db" stroke-width="2"/>
  <circle cx="250" cy="125" r="100" fill="rgba(231,76,60,0.3)" stroke="#e74c3c" stroke-width="2"/>
  <text x="110" y="130" text-anchor="middle" font-size="14">Gato</text>
  <text x="290" y="130" text-anchor="middle" font-size="14">Pássaro</text>
  <text x="200" y="130" text-anchor="middle" font-size="12">Gato ∩ Pássaro</text>
</svg>


#### Independentes / Dependentes

Então entendendo que para saber a probabilidade de dois eventos ocorrerem ao mesmo tempo eu preciso calcular a interseção entre eles, como faço pra calcula-lo, sendo que só vimos até a agora a união \(\cup\)? A palavra chave aqui é "e", ou sejam, qual a probabilidade da imagem ter um gato <u>e</u> um pássaro ao mesmo tempo? 
$$P(gato \cap pássaro) = P(gato) \cdot P(pássaro)$$, ou seja, se a \(P(gato) = 0.3\) e \(P(pássaro) = 0.4\), então 
$$P(gato \cap pássaro) = 0.3 \cdot 0.4 = 0.12 = 12\%$$

Porém isso é valido apenas para eventos independentes, ou seja, eventos que não influenciam um ao outro. 

Verifiquemos outro exemplo. Suponha que adicionemos a esse modelo a detecção de carros e estradas. Suponhamos que possuímos 100 imagens, e que 20 possuem um carro, 10 possuem uma estrada, e 5 possuem ambos.
Então:
$$P(carro) = \frac{20}{100} = 0.2 = 20\%$$
$$P(estrada) = \frac{10}{100} = 0.1 = 10\%$$ portanto, de acordo com nossos cálculos:
$$P(carro \cap estrada) = P(carro) \cdot P(estrada) = 0.2 \cdot 0.1 = 0.02 = 2\%$$, porém, na nossa contagem, vimos que temos 5 imagens que possuem ambos, ou seja :
$$P(carro \cap estrada) = \frac{5}{100} = 0.05 = 5\%$$

Por que os cálculos não bateram? Porque se analisarmos o contexto, realmente a probabilidade de uma imagem de um carro ter também uma estrada não é zero, gera uma certa dependência entre eles. Daí vem a importância de analisar o contexto dos seus dados.

#### Por que é importante entender a diferença entre eventos independentes e dependentes?

{{< alert icon="triangle-exclamation" >}}

Dependendo do modelo de Machine Learning que você utilize, a dependência entre eventos/features impacta diretamente na performance do modelo. 
{{< /alert >}}


## Probabilidade Condicional

Sabendo então que alguns eventos podem ser dependentes do outro, como nosso caso de carro e estrada, podemos calcular a probabilidade de evento ocorrer sabendo (dado) que outro evento ocorreu, ou seja, qual a probabilidade de carros aparecerem em uma imagem sabendo que já temos uma estrada. Isso é chamado de probabilidade condicional:
$$P(A | B) = \frac{P(A \cap B)}{P(B)}$$, no nosso caso:

$$P(carro | estrada) = \frac{P(carro \cap estrada)}{P(estrada)}$$, usamos o símbolo \( | \) para indicar "dado que", ou sejam probabilidade de ter um carro dado que já temos uma estrada.
Assim sendo:
$$P(carro | estrada) = \frac{0.05}{0.1} = 0.5 = 50\%$$ 
{{< alert icon="triangle-exclamation" >}}
ou seja, a probabilidade de ter um carro em uma imagem sabendo que já temos uma estrada é de 50\%, o que é bem diferente da probabilidade de ter um carro sem essa informação, que era de 20\%.
{{< /alert >}}

## Resumo

Nesse artigo vimos a importância de entender a diferença entre eventos mutuamente exclusivos, não mutuamente exclusivos, independentes e dependentes, e como isso impacta diretamente na performance de modelos de Machine Learning. Vimos também como calcular a probabilidade de um evento sabendo que um outro evento dependente já ocorreu.

No próximo artigo, vamos falar sobre o Teorema de Bayes! Fique ligado! Caso queira receber um alerta quando um artigo for publicado, se inscreva abaixo.

## Referências
- [Mathematics for Machine Learning and Data Science - deeplearning.ai](https://www.deeplearning.ai/courses/mathematics-for-machine-learning-and-data-science/)
- [Probability and Statistics: The Science of Uncertainty - Michael J. Evans, Jeffrey S. Rosenthal](https://www.amazon.com/Probability-Statistics-Science-Uncertainty-Second/dp/1466575570)
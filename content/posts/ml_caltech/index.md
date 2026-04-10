+++
date = '2026-04-10T13:07:47-03:00'
draft = true
title = 'Curso Learning from Data - Caltech'
series = ["Machine Learning"]
tags = ["Machine Learning", "IA", "ML"]
+++
{{< katex >}}

Como um das minhas metas de revisão e estudos para 2026, está o curso Learning from Data, oferecido pela Caltech. O curso é ministrado pelo professor [Yaser Abu-Mostafa](https://www.eas.caltech.edu/people/yaser) e tem todo o seu material disponível online.
Eu o estou acompanhando pela plataforma [EDX](https://www.edx.org/learn/machine-learning/caltech-learning-from-data-introductory-machine-learning), onde ele é oferecido gratuitamente. 

O curso vai focar bastante na base para um bom conhecimento.

- [Curso Learning from Data - Caltech](#curso-learning-from-data---caltech)
- [Epilogo](#epilogo)
  - [Mapa do Curso](#mapa-do-curso)
    - [Teoria](#teoria)
    - [Técnicas](#técnicas)
    - [Paradigmas](#paradigmas)
- [O Problema de Aprendizado](#o-problema-de-aprendizado)
  - [Dados Disponíveis](#dados-disponíveis)
  - [Um padrão existe](#um-padrão-existe)
  - [Não é possível criar um função matemática de maneira simples](#não-é-possível-criar-um-função-matemática-de-maneira-simples)
- [O Fluxo do Aprendizado](#o-fluxo-do-aprendizado)
- [Referências](#referências)

## Curso Learning from Data - Caltech
O curso é uma introdução ao aprendizado de máquina, e aborda os seguintes tópicos:

- Aula 1: O Problema de Aprendizado
- Aula 2: É Possível Aprender?
- Aula 3: O Modelo Linear I
- Aula 4: Erro e Ruído
- Aula 5: Treinamento versus Teste
- Aula 6: Teoria da Generalização
- Aula 7: Dimensão VC
- Aula 8: Dilema Viés-Variância
- Aula 9: O Modelo Linear II
- Aula 10: Redes Neurais
- Aula 11: Overfitting
- Aula 12: Regularização
- Aula 13: Validação
- Aula 14: Máquinas de Vetores de Suporte
- Aula 15: Métodos de Kernel
- Aula 16: Funções de Base Radial
- Aula 17: Três Princípios de Aprendizado
- Aula 18: Epílogo

## Epilogo

O professor Yaser começa pontuando que o curso falará de teoria matemática, porém focada na execução pratica de machine learning, ou seja, não serão cobertos muitos outros possíveis tópicos por questão de tempo.


### Mapa do Curso

#### Teoria
- Vapnik-Chervonenkis
- Viés-Variância
- Complexidade
- Inferência Bayesiana

#### Técnicas
**Modelos**
- Linear
- Redes Neurais
- Vetores de Suporte
- k-Nearest Neighbors
- Árvores de Decisão
- Processos Gaussianos
- Decomposição em Valores Singulares
- Modelos de grafos

**Métodos**
- Regularização
- Validação
- Agregação
- Processamento de dados

#### Paradigmas
- Supervisionado
- Não Supervisionado
- Reforço
- Ativo
- Online


## O Problema de Aprendizado

Essa matéria começa inicialmente com a definição do que é a essência do uso de machine learning. Ele usa o exemplo de um banco que quer aprovar um empréstimo, ou não para um cliente, baseado se ele é um bom pagador ou não.

A essencia, segundo o professor, sao as características que definem se um problema deve ser resolvido usando machine learning ou não. São elas:
- Um padrão existe
- Não é possivel criar um função matematica de maneira simples
- Existem dados disponiveis para aprender o padrão

{{< alert icon="comment" >}}
**Caso Real:** Já fui acionado para fazer uma analise de um possivel problema à ser resolvido com machine learning, que ao conversar com o gestor da área, o mesmo tinha os dados, porem todos em livros fisicos, ou seja até que os mesmo fossem digitalizados, o projeto de machine learning não poderia ser iniciado. Sendo assim,  a pergunta de se existem dados, é de extrema importancia!
{{< /alert >}}


### Dados Disponíveis

O Banco possui as informacoes e historico dos clientes, como idade, renda, salário, tempo de carteira de trabalho, debitos atuais, etc. Vamos chamar isso de dados de entrada, ou input, e matematicamente de \(x\). 

O banco também tem o histórico de clientes que pagaram ou não os empréstimos, ou seja, a resposta, ou output,  \(y\).

A junção desses dados, ou dataset, seria 
$$(x_1, y_1), (x_2, y_2), ..., (x_N, y_N))$$ onde \(N\) é o número de clientes.

### Um padrão existe

É de se imaginar que exista um padrão nesses dados, ou seja, uma função que baseado nas características dos clientes, consiga prever se o mesmo é um bom pagador ou não. Chamaremos isso de função alvo, ou target function, \(f\), tal qual 
$$f: X \rightarrow Y$$ sendo \(X\) todos as informações historicas do cliente e \(Y\) a resposta se o cliente é um bom pagador ou não.


### Não é possível criar um função matemática de maneira simples

Como não é possivel criar uma função \(f\) simples, criamos uma hipótese, funçao
$$g: X \rightarrow Y$$ tal que seja uma aproximação de \(f\), ou seja, \(g \approx f\).

## O Fluxo do Aprendizado

E como fazemos para aprender a função \(g\)? O processo de aprendizado é o seguinte:

{{< mermaid >}}
graph TD
    A[Dados de Entrada (x)] --> B[Função Hipótese (g)]
    B --> C[Predição (g(x))]
    C --> D[Comparação com a Resposta Real (y)]
    D --> E[Erro]
    E --> F[Atualização da Função Hipótese (g)]
    F --> B
{{< /mermaid >}}






## Referências

- [Learning from Data - Caltech](https://work.caltech.edu/telecourse.html)


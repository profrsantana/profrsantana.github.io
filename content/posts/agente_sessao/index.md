+++
date = '2026-05-08T16:50:33-03:00'
title = 'Usando Memória de Sessão para manter o contexto em conversas com agentes'
series = ["Microsoft Agent Framework"]
series_order = 4
tags = ["MAF", "Agentes", "IA", "Microsoft"]
+++

## Memória de Sessão 

No último artigo, mostramos como adicionar ferramentas a agentes, para que ele possa executar ações, buscar informações ou tomar decisões. Mas e se quisermos que o agente lembre de informações fornecidas pelo usuário durante a conversa? É aí que entra a memória de sessão.

No exemplo anterior, todas as vezes que falamos com o agente, ele executava as tarefas necessárias, porém se conversássemos novamente, ele não lembraria do que falamos anteriormente, ou seja, ele não teria um contexto de conversa. 
Façamos um teste. Após perguntar qual a temperatura em São José dos Campos, vou perguntar, de qual cidade você acabou de me falar a temperatura.

```python
result = await agente.run("Qual é a temperatura em São José dos Campos?")
print(f"Agente: {result}")

result = await agente.run("De qual cidade você acabou de me falar a temperatura?")
print(f"Agente: {result}")
```

```bash
Agente: A temperatura atual em São José dos Campos é de 21,2°C.
Agente: Ainda não falei sobre a temperatura de nenhuma cidade. Que cidade você gostaria de saber a temperatura?
```
Veja que o agente não tem memória de sessão, ele não lembra que falamos sobre a temperatura de São José dos Campos, e responde como se fosse a primeira vez que falamos com ele.


## Usando a memória de sessão 

Para resolver esse ponto, o Microsoft Agent Framework tem uma funcionalidade de sessão, onde podemos centralizar as informações da conversa, para que o agente tenha acesso ao contexto como um todo, e não apenas a última mensagem.
Para isso, antes de iniciar a conversa com o agente, criamos uma sessão, usando o método `create_session()` do agente, e passando essa sessão como parâmetro para o método `run()`, assim o agente tem acesso a todas as informações da conversa, e pode lembrar de informações passadas anteriormente.


```python
sessao = agente.create_session()

result = await agente.run("Qual é a temperatura em São José dos Campos?", session=sessao)
print(f"Agente: {result}")

result = await agente.run("De qual cidade você acabou de me falar a temperatura?", session=sessao)
print(f"Agente: {result}")
```

```bash
Agente: A temperatura atual em São José dos Campos é de 21,2°C.
Agente: Eu falei sobre a temperatura de São José dos Campos.
```

{{< alert icon="circle-info" >}}
Os dados da sessão são mantidos em memória, ou seja, se o agente for reiniciado, a sessão é perdida e não se terá mais acesso ao contexto da conversa. 

{{< /alert >}}

No próximo artigo, vamos ver como usar memória de longo prazo, para que o agente possa lembrar de informações mesmo após ser reiniciado.

{{< alert icon="triangle-exclamation" >}}
Se estiver usando o chat do OpenAI, garanta que o nome do agente não tenha espaços, pois o padrão de nome de agentes deles não aceita espaços.

```python
agente = cliente_openai.as_agent(
    name="Agente_Previsao_do_Tempo",
    ...
)
```

{{< /alert >}}

## Resumo

Neste artigo, mostramos como usar a memória de sessão no Microsoft Agent Framework para manter o contexto em conversas com agentes. Vimos que, sem a memória de sessão, o agente não lembra das informações fornecidas previamente pelo usuário. Com o parâmetro de sessão, o agente pode acessar o contexto completo da conversa.

Acesse o código completo do agente com memória de sessão no meu repositório do GitHub, no link das referências.

Se inscreva na newsletter para receber os próximos artigos da série, onde vamos explorar mais funcionalidades do Microsoft Agent Framework.



## Referências

- [Repositório do códigos da série de artigos](https://github.com/profrsantana/maf)
- [Repositório do códigos desse artigo](https://github.com/profrsantana/maf/tree/main/agente_sessao)
- [Microsoft Agent Framework Learn](https://learn.microsoft.com/en-us/agent-framework/overview/?pivots=programming-language-python)
- [Microsoft Agent Framework GitHub](https://github.com/microsoft/agent-framework)
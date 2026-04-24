+++
date = '2026-04-24T18:10:51-03:00'
title = 'Adicionando ferramentas a agentes com o Microsoft Agent Framework'
series = ["Microsoft Agent Framework"]
series_order = 3
tags = ["MAF", "Agentes", "IA", "Microsoft"]

+++

## Adicionando ferramentas a agentes

No ultimo artigo, mostramos como criar um agente básico usando o MAF, porem se formos para a definição do que realmente é um agente, o exemplo anterior era somente um ChatBot, pois só respondia a uma pergunta do usuário.
Os agentes são definidos por usa capacidade de agir mediante uma solicitação, podendo usar ***ferramentas*** para executar ações, buscar informações, ou tomar decisões.

No exemplo que vamos gerar hoje, vamos criar um agente que tem acesso a uma ferramenta de previsão do tempo, onde o usuário pode perguntar "Qual a temperatura atual em São Paulo?" e o agente irá usar a ferramenta para obter a resposta e entregar para o usuário.

{{< alert icon="circle-question" >}}
Você pode estar se perguntando, por que usar um agente para isso, se um chatbot comum poderia responder a essa pergunta? A resposta é que LLMs respondem baseados em dados históricos que foram usados durante o seu treinamento, ou seja, ele não esta lendo os dados em tempo real. As ferramentas possibilitam que os agentes tenham acesso a informações atualizadas.
{{< /alert >}}


Existem vários tipos de ferramentas:


| Tipo| Descrição |
|---|---|
| Função | Código personalizado que agentes podem chamar durante conversas |
| Aprovação  | Aprovação de usuários (Human in the loop) para invocações de ferramenta |
| Interpretador de Código | Executar código em um ambiente isolado |
| Pesquisa de Arquivo | Pesquisar em arquivos enviados |
| Pesquisa na Web | Pesquisar a web por informações |
| MCP Hospedadas | Ferramentas MCP hospedadas pela Microsoft Foundry |
| MCP Locais | Ferramentas MCP em execução localmente ou em servidores personalizados |
| Foundry toolkit | Configurações de ferramentas hospedadas e gerenciadas em um projeto Foundry |

Para o artigo de hoje, vamos focar na criação de uma ferramenta do tipo função,  e nos próximos artigos vamos explorar os outros tipos de ferramentas.

### Criando uma ferramenta do tipo função


A função a ser criada tem a mesma sintaxe de uma função comum em Python, com algumas  anotações para que o MAF reconheça como uma ferramenta.

1- O decorador `@tool` é usado para marcar a função como uma ferramenta, e recebe alguns parâmetros como nome e descrição.

2- Os parâmetros da função recebem uma anotação do tipo `Annotated` do modulo `typing`, que recebe o __tipo do parâmetro__ e um objeto `Field` com a descrição do parâmetro, para que o MAF possa entender que tipo de dado será fornecido pelo usuário.

O código para obter a previsão do tempo aqui não é tão importante, como comentei o código pode ser qualquer tipo de função normal de Python, mas só para esclarecer, estamos usando a API de geocoding e a API de previsão do tempo da Open Meteo, que são gratuitas e não exigem autenticação, onde recebe de entrada as coordenadas de um local e retorna a temperatura atual.

A função completa ficaria assim:

```python
@tool(
    name="temperatura_atual",
    description="Obtenha a previsão do tempo para um local específico.",
)
def temperatura_atual(
    location: Annotated[
        str, Field(description="O local para obter a previsão do tempo.")
    ],
) -> str:
    with httpx.Client(timeout=10) as client:
        geo = client.get(
            "https://geocoding-api.open-meteo.com/v1/search",
            params={"name": location, "count": 1, "language": "pt"},
        ).json()

        if not geo.get("results"):
            return f"Não foi possível encontrar a localização '{location}'."

        local = geo["results"][0]
        lat, lon, nome = local["latitude"], local["longitude"], local["name"]

        meteo = client.get(
            "https://api.open-meteo.com/v1/forecast",
            params={
                "latitude": lat,
                "longitude": lon,
                "current": "temperature_2m",
                "timezone": "auto",
            },
        ).json()

        temp = meteo["current"]["temperature_2m"]

        return f"Temperatura atual em {nome}: {temp}°C."

```

## Adicionando a ferramenta ao agente

Depois de criada a função, o próximo passo é adicioná-la como uma ferramenta do agente, para isso usamos o parâmetro `tools` do agente, passando o nome da ferramenta dentro de uma lista.

E também mencionando no seu novo prompt que existe uma ferramenta que pode ser usada para responder perguntas sobre o clima, para que o agente saiba quando usar a ferramenta durante as conversas com os usuários.

```python
agente = cliente_openai.as_agent(
    name="Agente Básico para previsão do tempo",
    instructions='''Você é um assistente amigável 
    com acesso a ferramenta de previsão do tempo. 
    Use a ferramenta para responder perguntas sobre o clima. 
    Mantenha suas respostas breves.''',
    tools=[temperatura_atual],
)
```

{{< alert icon="circle-info" >}}
No agente desse código, diferente do anterior, estamos usando o cliente do OpenAI, mas o processo de criação do agente e adição de ferramentas é o mesmo para o cliente do Azure Foundry, veja o link nas referencias com o código completo.

{{< /alert >}}


E pronto, agora o agente tem acesso a ferramenta de previsão do tempo, e pode responder perguntas como "Qual a temperatura atual em São José dos Campos?" 

```python
result = await agente.run("Qual é a temperatura em São José dos Campos?")
print(f"Agente: {result}")
```

```bash
Agente: A temperatura atual em São José dos Campos é de 21,2°C.
```

## Resumo

Neste artigo vimos como criar uma ferramenta do tipo função usando o Microsoft Agent Framework, e como adicionar essa ferramenta a um agente para que ele possa usar usa-las caso seja necessário.

No próximo artigo vamos ver como manter o contexto de conversas do agente, para que ele possa lembrar de informações passadas durante a conversa.


## Referências

- [Repositório do códigos da série de artigos](https://github.com/profrsantana/maf)
- [Repositório do códigos desse artigos](https://github.com/profrsantana/maf/tree/main/agente_tools)
- [Microsoft Agent Framework Learn](https://learn.microsoft.com/en-us/agent-framework/overview/?pivots=programming-language-python)
- [Microsoft Agent Framework GitHub](https://github.com/microsoft/agent-framework)

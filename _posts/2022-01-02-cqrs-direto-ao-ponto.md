---
title: CQRS, direto ao ponto
author: Daniel Belintani
date: 2022-01-02 22:00:00 -0300
categories: [Programação, Direto ao ponto]
tags: [programação, direto-ao-ponto, CQRS, segurança-informação]
math: true
# image: /assets/img/posts/cqrs-direto-ao-ponto/thumbnail.png
---

Com todo o seu charme, essa é daquelas expressões em inglês que arrepia a espinha de qualquer iniciante, e que todo profissional quando compreende o conceito, repete com orgulhos nos olhos.
(veja abaixo como é a pronúncia)
{% include embed-audio.html src="/assets/audio/posts/2022-01-02-cqrs-direto-ao-ponto/CQRS.mp3" %}

CQRS é a abreviação de _Command and Query Responsibility Segregation_.\

O que isso quer dizer?

####**Não misture "leitura dos dados" com "gravação dos dados"!**

### Quando usar
**Sempre que possível**. O "papo" de _over-engineering_ não se encaixa tão bem aqui, uma vez que não é tão complexo assim.\
Claro, sem hipocrisia, numa distribuição orientada à _microservices_, existe chance de ser um trabalho chato e menos justificável.

### Como implementar
Existe duas técnicas, no qual vi ser as mais comuns:

1 - Criando classes distintas, separando propriedades editáveis de dados disponíveis para consulta.

```c#
    public class CreatePlayer
    {
        public string Name { get; set; }
        public string Alias { get; set; }
        public string DefaultPassword { get; set; }
    }

    public class UpdatePlayer
    {
        public string Name { get; set; }
        public string Alias { get; set; }
        public string Password { get; set; }
    }

    public class FindPlayer
    {
        public Guid ID { get; set; }
        public string Name { get; set; }
        public string Alias { get; set; }
        public DateTime CreatedTime { get; set; }
    }
```

2 -  Separando acessos distintos de leitura e escrita, de preferência com credenciais diferentes para acesso à base de dados.

Um método deve ser _Command_ ou _Query_, nunca ambos.\
**_Command_** se refere às funções de criação, alteração ou exclusão.\
E por eliminação, **_Query_** são as consultas.


### Benefícios
#### - **Princípio da responsabilidade única**
Ao separar os métodos, já encontrará o código quebrado para uma única responsabilidade, o que facilitará na implementação de cobertura de testes, e também na própria manutenção.

#### - **Dimensionamento Independente**
Caso tenha um _software_ com mais requisições de leituras do que gravação, é ideal usar dois bancos de dados separados, podendo dimensionar os seus modelos de forma independente.\
\
Além disso, podemos desnormalizar o banco de dados de leitura, o que resultará em consultas simples, junções menos complexas, e tempo de resposta rápido.

#### - **Separação de preocupação**
As regras de persistência e atualização dos dados não irão influenciar nas consultas, e entregar credenciais distintas trará menores preocupações no acesso aos dados.\
Não basta estar blindado ao "_sql-injection_", mas também a atenção para erros humanos, o que acontece com frequência em projetos de objetos dinamicamente mapeados por um ORM.


**CQRS** é simples, mas que traz preocupações reais do mundo corporativo, e este conceito será referenciado em outros textos futuros, principalmente sobre tópicos relacionados à segurança da informação.

---
title: O que é uma Graph API
author: Daniel Belintani
date: 2021-09-25 17:00:00 -0300
categories: [Programação, Direto ao ponto]
tags: [programação, graph-api, direto-ao-ponto]
math: true
---

Uma Graph API é uma [REST API](https://www.openapis.org/), porém, seguindo uma modelagem de dados entre *nodes* e *edges*, permitindo executar a chamada de várias entidades de forma encadeada, com um único *request*. Apesar de ser um pouco diferente, isso não significa que todas as especificações anotadas na [OpenAPI](https://spec.openapis.org/oas/latest.html) devam ser ignoradas, pelo contrário, segue fielmente as especificações de cada verbo http, por exemplo.

Não é raro a confusão entre o conceito de uma GraphAPI com o uso de [GraphQL](https://graphql.org/learn/), esta segunda sim, é bem diferente do convencional, e só disponibiliza um único acesso GET e outro POST, recebendo uma consulta na semântica da graphQL.

Na composição de uma Graph API temos:

- *nodes* — basicamente objetos individuais, como um Usuário, Página Conta ou Comentário
- *edges* — conexões entre uma coleção de objetos com outros objetos
- *fields* — dados sobre um objeto.


### Object ID's

Os _nodes_, por representarem objetos individuais, obrigatoriamente possuem, cada um, a referência para um ID único no sistema inteiro. Assim sendo, para obter informações de um objeto, basta consultar diretamente pelo seu ID. Não precisa especificar o seu tipo na chamada.

```javascript
GET 'HOST/{node-id}'
```
### Fields

Para obter outros dados do objeto além do ID, é necessário especificar explicitamente na consulta, pelo parâmetro chamado _fields_.

```javascript
GET 'HOST/{node-id}?fields={var1},{var2}'
```

### Edges

Os relacionamentos entre objetos são encontrados pelas _edges_. Por padrão, elas retornam apenas ID's, mas assim como é para os _nodes_, o parâmetro _fields_ pode ser utilizado para retornar propriedades específicas em cada nível.

```javascript
GET 'HOST/{node-id}/{edge}?fields={var1},{var2}...'
```

### Exemplo → Facebook

Para exemplificar, apresento abaixo alguns exemplos de consultas reais do Facebook, que implementa em suas chamadas REST o conceito de Graph API.

Obter as contas de anúncio do usuário corrente, com nome da conta e o limite de gastos.

```javascript
GET 'https://graph.facebook.com/v11.0/me/adaccounts?fields=id,name,spend_cap'
```

"me" é o ***node***, "adaccounts" é a ***edge*** , e "id,name,spend_cap" são os ***fields***.

Para cada conta de anúncio, é possível executar outra chamada para encontrar alguns dados das campanhas que estão dentro das contas de anúncio.

```javascript
GET '.../v11.0/{adaccount-id}/campaigns?fields=id,name,objective,effective_status'
```

"{adaccount-id}" é o ***node***, "campaigns" é a ***edge***, e "id,name,objective,effective_status" são os ***fields***.

No exemplo acima, se o usuário possuir 30 contas de anúncio, a chamada para buscar as campanhas deve ser invocada 30x.

Por isso, uma Graph API possui o grande trunfo: a busca encadeada.

```javascript
GET '.../v11.0/me/adaccounts?fields=id,name,spend_cap,campaigns{id,name,objective,effective_status}'
```

Se você pensou "parece mágica", bem-vindo ao clube!

Esta mesma explosão ocorreu-me em 2013, quando comecei a trabalhar com as [Graph API's do Facebook](https://developers.facebook.com/docs/graph-api/overview)

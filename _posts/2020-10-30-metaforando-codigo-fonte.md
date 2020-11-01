---
title: Metaforando, uma análise não-funcional
author: Daniel Belintani
date: 2020-11-01 10:30:00 -0300
categories: [Programação, Metaforando]
tags: [código, programação, comentário, metaforando]
# image: /assets/img/posts/metaforando-codigo-fonte/thumbnail.png
---
Atenção: Todas as piadas são referências ao [canal metaforando, do Vitor Santos](https://www.youtube.com/channel/UCh7TUTXojlE8vRtb-EnuDzw).
![Desktop View](/assets/img/posts/metaforando-codigo-fonte/ministerio-prog-avancada.png)

Eu sou [**Daniel Belintani**](https://belintani.com/), perito não-profissional de micro expressões regulares.

### “Código nunca mente. Já os comentários as vezes o fazem.”

Acredito que a primeira vez que eu vi esta frase foi em 2009, e naquele momento a minha cabeça explodiu! Desde então, nunca mais documentei um código "só por documentar". Ao procurar o texto original e [atribuir corretamente os louros](https://ciberduvidas.iscte-iul.pt/consultorio/perguntas/a-expressao-ficar-com-os-louros/28930) ao seu criado(a), só encontrei o famoso [Ron Jeffries](https://en.wikipedia.org/wiki/Ron_Jeffries), quando divulgou a frase ao [tweetar](https://twitter.com/ronjeffries/status/949400218092687361), em 2018.

Diagnosticando um cenário, na prática, sobre uma função que irá finalizar um carrinho de compras.
![Desktop View](/assets/img/posts/metaforando-codigo-fonte/congruentes.png)
Até o momento, a análise realmente prova de que os comentários mostram descritivos **congruentes**. Apesar destes comentários serem completamente inúteis dado a sua redundância.

Seria aceitável que este código na sequência precise começar a verificar se o carrinho não está vazio:
![Desktop View](/assets/img/posts/metaforando-codigo-fonte/alteracao-1.png)

Conforme o protocolo SPAMS, podemos observar que o descritivo da função "finaliza um carrinho, ou mostra mensagem de erro" já apresenta o seu primeiro comportamento **incongruente**. Fica evidente o não comentário direto, ao analisar que a função evita dizer: "eu retorno warning". Isso poder ser justificado por um simples esquecimento dos fatos pelo(a) programado(a).  
![Desktop View](/assets/img/posts/metaforando-codigo-fonte/nao-responder-diretamente.png)

Esta alteração no código também apresentou uma expressão de IDH (início de um histórico) na L9 seguido de um FDH (fim de histórico) na L14. O que de fato, não é um comentário bem-visto pela comunidade, sendo que há controladores de versão (ex: git) para exercer tal função.
![Desktop View](/assets/img/posts/metaforando-codigo-fonte/idh-fdh.png)

Os comentários são então removidos no PR (pull request), mas alguns meses depois, um BUG traz uma nova pessoa para este código, e sem nenhum apego emocional, temos a alteração abaixo:
![Desktop View](/assets/img/posts/metaforando-codigo-fonte/vergonha.png)
Vemos então um comentário desesperado, guiado pelo sentimento de vergonha ao fazer uma gambiarra desnecessária. É comum que pessoas culpadas deixem comentários como rastro dos seus crimes, na crença de que ganhou um "passe-livre da prisão" ao justificar-se com um comentário.

Outro comportamento de um comentário que tende a ser mentiroso, é o excesso de ~~tensao~~ textão, onde é adicionado um comentário longo para que ninguém leia. Este comentário, muito provavelmente não sofrerá a devida alteração quando algo mudar na regra de negócio.
![Desktop View](/assets/img/posts/metaforando-codigo-fonte/textao.png)
Desconfie também de comentários que forçam a sua [IDE](https://www.redhat.com/pt-br/topics/middleware/what-is-ide) (ferramenta de escrever código) a minimizar parte de códigos, isso pode ser considerado "afastamento e quebra de contato visual", muito utilizado por truques de mágicas.

Comentários podem ser mentirosos. Cuidado. Porém, existem comentários úteis:
- Comentários em acessos públicos. Se o código for "fechado", seja num servidor, ou em uma SDK, quem desenvolveu tem o dever de documentar e manter atualizado a explicação de como utilizar e qual a sua função. Para APIs a solução mais comum é o [swagger](https://swagger.io/).
- Comentários de TODO. Nunca deixe de anotar parte do código que ficou faltando algo ou que pode ser refatorado. Basta adicionar "TODO: o que fazer" nas linhas de referência.

Lembrando também que esse texto é um estudo, no qual venho na condição de perito dar uma visão, mas essa não é uma cartada final muito menos a verdade absoluta, é apenas uma análise.

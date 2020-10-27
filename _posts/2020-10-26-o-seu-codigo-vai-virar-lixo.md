---
title: O seu código vai virar lixo
author: Daniel Belintani
date: 2020-10-26 12:00:00 -0300
categories: [Carreira]
tags: [carreira, programação, startup, cleancode]
math: true
# image: /assets/img/o-seu-codigo-vai-virar-lixo/thumbnail.png
---

Este título não se trata apenas de um [clickbait](https://pt.wikipedia.org/wiki/Clickbait), mas sim um tema sensível, uma vez que pode atacar diretamente o ego de quem vem a construir _software_ ao deparar com o fim trágico e eminente do seu trabalho.

Participei ativamente de pelo menos 250 contratações de devs nos últimos anos, e considerando uma média de 30 entrevistas presenciais para cada posição, estamos a falar de algo em torno de 7.500 reuniões de recrutamento. Acredite ou não, uma das frases que mais escuto dos participantes é: 
> "Eu não faço código para ir parar no lixo".

Algo interessante é que esta frase sempre traz o gatilho que preciso para compartilhar um pensamento que propago há alguns anos: "Todo o seu código, ou boa parte dele, vai virar lixo". A reação de espanto ou choque de realidade é instantânea para quem escuta pela primeira vez, e claro, ao mesmo tempo, já utilizo para avaliar comportamento ao ser confrontado(a) em algo que sempre repetiu a carreira toda.

A explicação é relativamente simples. Quem acompanhou o meu outro texto "[quem não inova, morre](https://belintani.com/posts/quem-nao-inova-morre/)" já sabe que trabalhei utilizando [Adobe Flex Builder](https://www.adobe.com/br/products/flex.html), para gerar websites em flash, e que sofri um pouco criando widgets [J2ME (java micro edition](https://www.java.com/pt-BR/download/help/whatis_j2me.html)). Também criei soluções web com [applets](https://docs.oracle.com/javase/tutorial/deployment/applet/security.html) (java), trabalhei em sistemas criando _interfaces_ no Microsoft Access 95, e até em um ERP inteiro desenvolvido em Visual Basic 6.0, tudo isso há mais de 10 anos atrás. E se alguém julga que não poderia ser pior, desenvolvi um sistema inteiro em Microsoft Silverlight (competidor do flash), e até já utilizei uma "linguagem de programação própria" de uma empresa privada.

Isso quer dizer que, apenas do meu trabalho, milhares de horas de programação, e incontáveis linhas de código, foram parar no lixo.

Alguns fatores responsáveis por direcionar códigos para a lixeira:

- **Qualidade:** Se o código não for legível, é mais fácil apagar e escrever novamente
- **Desempenho:** Se o código não está devidamente desacoplado (independente) e preparado para escalar, outro virá para fazer o mesmo processo mais rápido
- **Tecnologia:** O fator mais injusto de todos. Ao atualizar frameworks e linguagens, novas opções entram no mercado, até que um dia o código é depreciado por completo.


Uma das missões de todo bom profissional na área é justamente **aumentar a longevidade do código o máximo possível**, certo? 

O primeiro passo que recomendo é justamente o reconhecimento. Saber que o código um dia será apagado, o que precisa ser feito para garantir que ele atenda o seu propósito pelo maior tempo possível.

Adicionar [teste unitário](https://softwaretestingfundamentals.com/unit-testing/) no seu código é um excelente início. Sem ele, é quase certo que outra pessoa vai achar mais fácil apagar e reescrever a sua função. Todavia, se o código estiver com 100% de cobertura, com todos os casos mapeados, a probabilidade do código "sobreviver" a manutenção é exponencialmente maior. O ponto de atenção é que teste unitário mal elaborado/pensado, provavelmente vai parar no lixo a cada nova alteração.

Utilizar tecnologia de ponta é o mais óbvio. Se um ciclo de vida de 3-5 anos já é considerado longo para um _software_, o que acontece se for utilizado uma linguagem de programação ou framework com 2 anos já atrasado? O código vai parar no lixo 2 anos mais cedo, simples assim! Nunca inicie um projeto utilizando tecnologia antiga, por mais que "a curva de aprendizado vá tirar-lhe da zona de conforto", o compromisso em lutar contra a remoção do seu código tem que ser mais relevante. E se, o que lhe limita é a tecnologia já adotada na empresa, termine este texto, agende um compromisso de 1 hora na sua vida, PARE TUDO, e vá ler sobre [microsserviços](https://microservices.io/) e virtualização com [docker](https://www.docker.com/).

Além disso, mantenha um código elegante. Estude MUITO a tecnologia do momento, pois, sempre estará em aprimoramento, uma vez que concordou com tudo que escrevi até aqui, e logo, estará anualmente se atualizando com novas tecnologias. O trabalho árduo não trará uma visibilidade tão imediata da sua maturidade, mas posso afirmar-lhe que após 10 anos seus códigos serão naturalmente elegantes. Alguns materiais mais antigos podem ajudar no pontapé para quem está a iniciar, como o [Clean Code](https://books.google.com.br/books/about/C%C3%B3digo_Limpo.html?id=GXWkDwAAQBAJ), e o [Clean Architecture](https://books.google.com.br/books?id=8ngAkAEACAAJ), mas realmente o que mais recomendo, é a participação ativa na comunidade. Abrace um ou dois projetos _open source_ grandes, tenho certeza que aprenderá muito só de observar outros códigos.

Para quem aguardou até aqui para discordar, sim, existem vários códigos que se mantém vivos por décadas, estes normalmente associados a código de baixo nível (alta _performance_), extremamente objetivos (elegante), e testáveis. Confie em mim, eles só estão preparados para longevidade, mas eles vão para a lixeira algum dia, é questão de tempo, nem que seja numa era da computação quântica.

Afinal, qual a longevidade buscar? A fórmula é bem simples. **Custo x Benefício**.

Reconhecendo o fracasso iminente do seu código, e o esforço em adequá-lo aos padrões da longevidade, coloque na balança. 
Se em três horas for possível produzir um código que irá durar seis meses, logo, em doze horas deveria ser criado algo para permanecer por mais de dois anos. Caso contrário, não é tão vantajoso assim.

Contudo, isso depende. Em _startups_, a grande armadilha mora no [_over engineering_](https://www.codesimplicity.com/post/what-is-overengineering/). Muitas vezes devs com muita experiência de mercado insistem em dedicar **200 horas** em criar uma funcionalidade que poderia ser desenvolvida em **40 horas** (e durar apenas um ano). Para tirarmos vantagem (CxB), o código precisa durar cinco anos. E o mais bizarro é que normalmente são códigos preparados para tal longevidade. Mas nem tudo são flores e tão simples.

O que **erroneamente** acaba a ficar de fora da equação é o [_time to market_](https://en.wikipedia.org/wiki/Time_to_market). Uma _startup_ precisa sempre estar de olho em aproveitar o momento. Não adianta negar, todos queremos o famoso [unicórnio](https://www.inacademy.eu/blog/whats-a-unicorn-startup-company/), e quando buscamos crescimento exponencial, é mais vantajoso ter um código que irá durar um ano, mas que é desenvolvido em uma semana, do que uma funcionalidade que vai permanecer imutável por cinco anos levando mais de um mês para ser construída. Afinal, é _startup_, a cada trimestre o foco ainda pode mudar, e uma funcionalidade nova poderá trazer "aquele cliente" que salvará as contas do mês.
   
Isso não é um passe livre para criar um monte de código lixo! Afinal, queremos um código que vai parar na lixeira, e não que já nasce lá. 

1. Esteja preparado(a) para criar um código que irá durar muito, será útil algumas vezes.
2. Entenda a solução que está a construir e o momento de mercado. Não seja apenas um peão neste jogo de xadrez, entenda o projeto na totalidade.
3. Por fim, comunique a sua estratégia para os colegas, não faça um código rápido, e nem extenso, sem antes compartilhar a sua visão com os demais membros do projeto, e tomando a decisão no coletivo.

---
title: SOLID, direto ao ponto
author: Daniel Belintani
date: 2021-06-05 11:00:00 -0300
categories: [Direto ao ponto]
tags: [programação, orientacao-objeto, direto-ao-ponto]
math: true
# image: /assets/img/posts/solid-direto-ao-ponto/thumbnail.png
---

##### A saga de “direto ao ponto” apresenta alguns textos rápidos para desmistificar assuntos simples. 

## S O L I D
Ao trabalhar efetivamente com Programação Orientada a Objetos (POO), provavelmente os 5 princípios SOLID já estão presentes no dia a dia, mesmo que de forma não intencional.

### **S — Single Responsiblity Principle** 
(Princípio da responsabilidade única)

Ao separar a arquitetura do projeto em camadas, provavelmente as suas classes já são quebradas, mantendo-as com uma responsabilidade única. 

![Desktop View](/assets/img/posts/solid-direto-ao-ponto/store-splitted.png)

### **O — Open-Closed Principle**.
(Princípio Aberto-Fechado)

Defina as ações do sistema em _interfaces_ e referencie-as nas funções ao invés de trabalhar com as classes originais.

Exemplificando, considere `Enumerable` uma _interface_ para utilizar na função de `Count()` que avança para a função `Next()` até acabar a lista. Em nenhum momento um array de um objeto foi citado, e a função `Count()` trabalha exclusivamente com a _interface_.

````c#
public int Count(Enumerable e){
    int i = 0;
    do {
        i++;
    } while(e.Next());
}
````

### **L — Liskov Substitution Principle**.
(Princípio da substituição de Liskov)

Quando uma classe estende outra, trabalhe a classe de mais alto nível nas funções. Assim sendo, se existir a classe `Eletronico`, e as classes filhas `Televisão` e `Laptop`, sempre dê preferência por trabalhar funções que manipulam `Eletronico`.

````c#
public class Eletronico {
    public void Ligar();
}

public class Televisao : Eletronico {
    public bool suportaHDTV;
}

public class Laptop : Eletronico {
    public byte portasUSB;
}

public class SistemaIntegrado {

    public void LigarSistemas(Eletronico[] es) {
        foreach(e in es) {
            e.Ligar();
        }
    }
}
````

### **I — Interface Segregation Principle**.
(Princípio da Segregação da Interface)

Não obrigue uma classe importar uma _interface_, se a mesma não for implementar todo o contrato.

Considere duas classes, `ContaCorrente` e `ContaPoupanca`, onde ambas podem receber depósitos e recebem a implementação da _interface_ `Depositavel`. Caso seja necessário rentabilizar o dinheiro da `ContaPoupanca`, não adicione a função `CalcularLucro` na mesma _interface_, afinal, a classe `ContaCorrente` não irá implementar tal calculo. Crie uma _interface_ `Rentavel` e atribua apenas nos tipos de conta que terão rentabilidade.
````c#
public interface Depositavel {
    public function Depositar(int valor);
}

public interface Rentavel {
    public void CalcularLucro();
}

public class ContaCorrente : Depositavel {
    public void Depositar(int valor) {
        // depositar em conta corrente
    }
}

public class ContaPoupanca : Rentavel, Depositavel {

    public void CalcularLucro() {
        // calculo base da poupanca
    }

    public void Depositar(int valor) {
        // depositar em conta poupanca
    }
} 

````

### **DIP — Dependency Inversion Principle**.
(Princípio da Inversão de Dependência)

Encapsule qualquer classe externa dentro de uma classe própria, e passe este objeto para as classes que irão utilizar. Um injetor de dependência já garante a inversão de dependência.

Por exemplo, não deixe a função `EnviarEmail` responsável por decidir como obter o `Remente`, e em vez disso, já receba pronto as instâncias necessárias.

````c#
public bool EnviarEmail(Remetente r, Destinatario d, Formatador f, EmailManager em) {
    return em.Send(r.All(), d.All(), f.ToEmailEncode());
}
````

### Por hoje é só pessoal!
Continue a acompanhar as próximas publicações para abordarmos mais temas de forma descomplicada e direto ao ponto.

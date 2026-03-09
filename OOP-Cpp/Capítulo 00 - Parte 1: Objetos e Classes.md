# Capítulo 0: Objetos e Classes

Agora que vocês já conheceram os mecanismos básicos do C++, vamos começar a pensar um pouco diferente. Entendemos como o C++ funciona de forma *procedural*. Agora veremos as coisas pelo prisma da **Orientação a Objetos**.

Neste capítulo, abordaremos os conceitos de *objetos* e *classes* e como podemos usá-los para dar ao nosso código escalabilidade e reutilizabilidade.

## 0.1 O que é a *Programação Orientada a Objetos*?

*"Veremos as coisas pelo prisma da Orientação a Objetos"*. Mas o que **é** a Orientação a Objetos? Onde vive? O que come?

A Programação Orientada a Objetos -- *ou POO, para os mais íntimos* -- nada mais é do que
um conjunto de ideias, conceitos e regras. Um padrão que usamos para resolver alguns tipos
de problema específicos. Na orientação a objetos, tentamos representar entidades que podemos
ver na vida real, junto das suas características e comportamentos.

Digamos, por exemplo, que queremos representar um *gatinho* no código >\^-\^<.

Na vida real, gatinhos têm características que são comuns a todos os outros gatos, como bigodes, garras, orelhas e etc. De mesmo modo, cada gato tem características próprias da sua raça. Um gato siamês tem uma pelagem naturalmente diferente de um ragdoll. Mesmo gatos da mesma raça podem diferir na cor dos olhos ou no padrão da pelagem. Além disso, gatos podem expressar comportamentos como miar, pular, arranhar as coisas, empurrar objetos de superfícies, e por aí vai.

Com tantas características comuns e divergentes, como então podemos representar esse gatinho
no nosso programa?

## 0.2 O que são *classes*?

Para criarmos um gatinho, primeiro precisamos saber como representar gatos em geral. Classes
são como um molde que usamos para criar vários objetos semelhantes, mas diferentes. Elas permitem agruparmos objetos com um mesmo conjunto de características (**atributos**) e comportamentos
(**métodos**). 

No nosso caso, a espécie "gato" é a classe. Gatito, o gatinho que queremos representar, seria
uma **instância concreta** -- ou melhor, um *objeto* -- dessa classe.

A classe é quem determina quais são os elementos comuns aos objetos que a instanciam, enquanto
o objeto vai guardar as informações específicas sobre ele. Assim, a classe Gato teria o número
de patas que um gato possui ou a classe biológica *(mamífero)* à qual os gatos pertencem como atributos **estáticos** -- pertencentes a todos os membros da classe e não a uma instância --
e raça, nome e idade como atributos de instância. Também contém os métodos que podem ser chamados pelos objetos, como miar, e o que esse método fará efetivamente quando for chamado.

```cpp
classe Gato {
   //----- ESTÁTICOS ----- //
   atributo mamifero = true;
   atributo numero_patas = 4;

   //--- NÃO-ESTÁTICOS ---//
   atributo nome;
   atributo idade;
   atributo raca;

   void miar(){
      cout << "Miau!!" << endl;
   }
}
```

## 0.3 O que são *objetos*?

Já os objetos são, basicamente, ocorrências específicas das entidades que tentamos representar. Eles instanciam uma classe e guardam informações que não valem para todas as ocorrências daquela classe em atributos não-estáticos.

Desse modo, se definirmos o Gatito como um objeto da classe gato, podemos determinar e acessar
as informações sobre o Gatito (como raça, cor do olho e do pelo). Além disso, podemos saber que
o Gatito tem 4 patas e é mamífero, afinal ele é um Gato. Ainda, ele pode fazer uso de alguns métodos da classe Gato, afinal *todo gato pode miar*, mas quem mia de fato é o Gatito.

Aqui vão alguns exemplos de como atribuir um valor aos atributos de um objeto. Não recomendo que tente ainda, afinal **vai gerar erro**. Ainda vamos aprender alguns conceitos necessários para, de fato, criar classes e objetos. 

```cpp
   //Cria o objeto
   Gato gatito;

   //Determina o valor desses atributos
   gatito.nome = "Gatito";
   gatito.idade = 7;
   gatito.raca = PERSA;

   //Chama o método e executa seu código
   gatito.miar();
```

A seguir, um esquema visual para ajudar a entender a relação entre classes e seus objetos:

![Esquema visual representando três objetos da classe Gato. Cada objeto tem o mesmo número de patas (determinado pela classe), mas nome, idade e raça diferentes.](./imagens/cap000\ -\ img1.png)
   
## Conclusões

   Nesta primeira parte do capítulo, conhecemos alguns conceitos na teoria. Não se assuste. Em breve nos aprofundaremos nesses conceitos. Em sequência, vamos entender um pouco melhor sobre o que são construtores e como escrevê-los, além de algumas especificidades do C++. Fique de olho e não perca a Parte 2!
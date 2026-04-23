# Capítulo 01: Abstração e Encapsulamento

## 1.1 Modificadores de acesso

No que tange aos modificadores de acesso, certamente você já se deparou com algumas declarações adicionais em **atributos** e **métodos** em um código orientado a objetos. Estamos falando aqui daquelas palavras que aparecem antes dos tipos e dos nomes. Eles são os benditos **Modificadores de Acesso** e são bem importantes, diga-se de passagem.

O nome passa uma boa intuição a respeito do que seria isso. É um estabelecimento a respeito do quão acessível um bloco de código será para o restante da estrutura de um projeto. Eles controlam a visibilidade dos membros de uma classe.

No caso, em **C++**, temos três tipos diferentes:

### Public

Especificadores públicos fazem com que **atributos** e **métodos** sejam acessíveis em **toda a parte**. Ou seja, aqui não tem restrição nenhuma. Qualquer classe, função, em qualquer arquivo do projeto, pode acessar um atributo/método público de alguma classe em específico.

A **sintaxe** funciona da seguinte maneira:

```cpp
#include <iostream>
#include <string>

class Banda {
public:
    std::string nome;
};
```

Ou seja, digitamos `"public:"` na linha acima dos atributos/métodos que desejamos tornar públicos. Diferente de outras linguagens como `Java`, no `C++` precisamos declarar apenas uma vez e agrupá-los. Por exemplo:

```cpp
class Banda {
public:
  std::string nome;
  int anoFundacao;
  std::vector<std::string> listaDeMusicas;

  void imprimeListaDeMusicas(std::vector<std::string> listaDeMusicas) {
    for (int i = 0; i < listaDeMusicas.size(); i++) {
      std::cout << listaDeMusicas[i] << std::endl;
    }
  }
};
```

E se quiséssemos colocar a nossa classe em um arquivo separado e utilizar ela diretamente na `main.cpp`? O uso do `public` possibilita isso.

Vamos criar um arquivo separado, chamado `Bandas.cpp` e colocar o nosso código acima nele (e aproveitar para adicionar um construtor para nossa classe):

```
Bandas.cpp
```

```cpp
#include <iostream>
#include <string>
#include <vector>

class Banda {
public:
  std::string nome;
  int anoFundacao;
  std::vector<std::string> listaDeMusicas;

  Banda(std::string nome, int anoFundacao,
        std::vector<std::string> listaDeMusicas) {
    this->nome = nome;
    this->anoFundacao = anoFundacao;
    this->listaDeMusicas = listaDeMusicas;
  }

  void imprimeListaDeMusicas() {
    for (int i = 0; i < listaDeMusicas.size(); i++) {
      std::cout << listaDeMusicas[i] << std::endl;
    }
  }
};
```

Agora, vamos incluir ele no nosso `Main.cpp` e brincar com a programação:

```
Main.cpp
```

```cpp
#include "Bandas.cpp"
#include <iostream>
#include <string>
#include <vector>

int main() {
  Banda RATM("Rage Against The Machine", 1995,
             {"Bombtrack", "Killing in the Name", "Take the Power Back"});

  RATM.imprimeListaDeMusicas();

  return 0;
}
```

O compilador, em nenhum momento, reclamará do que fizemos aqui (pelo menos, é o que esperamos).

### Protected

Aqui, começamos a colocar algumas restrições nas coisas. Diferentemente do `public`, o `protected` faz com que métodos/atributos sejam **acessíveis apenas na própria classe e nas suas classes derivadas**. O que são classes derivadas? Já já vamos mostrar!

Na nossa classe `Banda`, vamos colocar um novo atributo, só que dessa vez ele não será público:

```
Bandas.cpp
```

```cpp
class Banda {
protected:
  std::string genero;

public:
  std::string nome;
  int anoFundacao;
  std::vector<std::string> listaDeMusicas;

  Banda(std::string nome, int anoFundacao,
        std::vector<std::string> listaDeMusicas, std::string genero) {
    this->nome = nome;
    this->anoFundacao = anoFundacao;
    this->listaDeMusicas = listaDeMusicas;
    this->genero = genero;
  }

  void imprimeListaDeMusicas() {
    for (int i = 0; i < listaDeMusicas.size(); i++) {
      std::cout << listaDeMusicas[i] << std::endl;
    }
  }
};
```

Colocamos um atributo protegido chamado de `genero`. Agora, vamos adicionar uma classe derivada:

```
Bandas.cpp
```

```cpp
//Classe derivada
class Metal : public Banda {
public:
  Metal(std::string nome, int anoFundacao,
        std::vector<std::string> listaDeMusicas, std::string genero)
      : Banda(nome, anoFundacao, listaDeMusicas, "METAL") {}

  void info() {
    std::cout << this->nome << std::endl;
    std::cout << this->anoFundacao << std::endl;
    std::cout << this->genero << std::endl;
  }
};
```

Explicaremos herança de um jeito melhor no próximo capítulo do curso. Mas, basicamente, criamos uma classe "filha" da classe "Banda". Ela herda as mesmas características da classe pai e, além disso, podemos adicionar novos atributos/métodos exclusivos da classe nova. Isso foi feito com a criação do método `info()` definido acima.

Além disso, aquelas linhas meio esquisitas logo depois de `public` dizem respeito ao construtor da nossa classe, que é único e será baseado no original. De maneira simples, elas dizem mais ou menos: "Esta nova classe aceitará esses atributos aqui e eles vão no construtor da classe pai, no qual eu me baseio, da seguinte maneira".

Prometemos que isso vai ser melhor explicado depois. Mas, achamos que, por ora, deu para entender.

Enfim. Se tentarmos acessar o atributo `genero` diretamente na `main()`, que está em um arquivo separado, teremos um problema na compilação. Fique livre para testar.

Porém, podemos realizar esse acesso através da nova classe, tendo em vista que ela tem uma função que imprime essa informação na tela.

Por exemplo:

```cpp
#include "Bandas.cpp"
#include <iostream>
#include <string>
#include <vector>

int main() {
  Metal RATM("Rage Against The Machine", 1995,
             {"Bombtrack", "Killing in the Name", "Take the Power Back"},
             "METAL");

  RATM.imprimeListaDeMusicas();
  RATM.info();

  return 0;
}
```

Compilando tudo, teremos a seguinte saída:

```
Bombtrack
Killing in the Name
Take the Power Back
Rage Against The Machine
1995
METAL
```

Utilizamos como exemplo um atributo, mas o mesmo vale para métodos. Fique livre para testar na sua máquina!

### Private

O especificador `private` faz com que atributos/métodos da classe sejam acessíveis apenas dentro da própria classe em si. Frequentemente, isso é utilizado para ocultar dados da parte externa.

Vamos adicionar um atributo privado na nossa classe `Banda`:

```
Banda.cpp
```

```cpp
class Banda {
private:
  std::string id;

protected:
  std::string genero;

public:
  std::string nome;
  int anoFundacao;
  std::vector<std::string> listaDeMusicas;

  Banda(std::string id, std::string nome, int anoFundacao,
        std::vector<std::string> listaDeMusicas, std::string genero) {
    this->id = id;
    this->nome = nome;
    this->anoFundacao = anoFundacao;
    this->listaDeMusicas = listaDeMusicas;
    this->genero = genero;
  }

  void imprimeListaDeMusicas() {
    for (int i = 0; i < listaDeMusicas.size(); i++) {
      std::cout << listaDeMusicas[i] << std::endl;
    }
  }
};
```

Do jeito que o código está, o que acontece se tentarmos acessar `id` na nossa classe filha?

```cpp
class Metal : public Banda {
public:
  Metal(std::string id, std::string nome, int anoFundacao,
        std::vector<std::string> listaDeMusicas, std::string genero)
      : Banda(id, nome, anoFundacao, listaDeMusicas, "METAL") {}

  void info() {
    std::cout << this->nome << std::endl;
    std::cout << this->anoFundacao << std::endl;
    std::cout << this->genero << std::endl;
    std::cout << this->id << std::endl; // Colocamos para printar aqui
  }
};
```

Teremos o seguinte erro de compilação:

```
Bandas.cpp: In member function ‘void Metal::info()’:
Bandas.cpp:43:24: error: ‘std::string Banda::id’ is private within this context
   43 |     std::cout << this->id << std::endl;
      |                        ^~
Bandas.cpp:7:15: note: declared private here
    7 |   std::string id;
      |               ^~
Bandas.cpp: In member function ‘void Metal::info()’:
Bandas.cpp:43:24: error: ‘std::string Banda::id’ is private within this context
   43 |     std::cout << this->id << std::endl;
      |                        ^~
Bandas.cpp:7:15: note: declared private here
    7 |   std::string id;
      |               ^~
```

Ou seja, inacessível para o exterior. Isso melhora bastante o encapsulamento de informações.

Pera, **encapsulamento**???

## 1.2 O que é encapsulamento?

## 1.3 Getters e Setters

## 1.4 O que é abstração?

No decorrer da nossa programação, muitas vezes podemos ter múltiplas classes que implementam os mesmos métodos. Porém, alguns deles, em específico, podem diferir a partir das características do que estamos projetando no nosso código.

Como podemos estruturar isso sem apelar para uma redundância _HardCoded_?

Em um código sem orientação a objetos, existem maneiras de realizar isso. Entretanto, muito provavelmente haveria a existência de um bloco de código externo àquilo que modelamos, tornando a nossa estruturação interdependente, prejudicando a escalabilidade e separação de responsabilidades no que diz respeito ao desenvolvimento.

Vamos pensar juntos.

E se quiséssemos, por algum motivo, programar diferentes animais caninos, com comportamentos em comum, mas que variassem em alguma coisa?

Em um código `main.cpp`, poderíamos fazer o seguinte:

```cpp
#include <iostream>
#include <string>

struct Canidae {
    std::string nome;
    int idade;
  // Imagine aqui algumas outras funções e variáveis que
  // são comuns a todos eles
  //  (...)
    std::string nome_acao;
    void executa() { std::cout << nome_acao << std::endl; }
};

Canidae Raposa = {"A Raposa ROUBA"};
Canidae Cachorro = {"O Cachorro TOMA"};
Canidae Lobo = {"O Lobo PEDE"};

int main() {
  Raposa.executa();
  Cachorro.executa();
  Lobo.executa();
  return 0;
}
```

No código acima, utilizamos uma estrutura e evitamos a redundância. Porém, tivemos que fazer a definição logo em seguida de cada um, de modo que a Raposa, o Cachorro e o Lobo são apenas declarações baseadas na nossa struct, e o print deles não é _inerentemente ligado a eles_.

Poderíamos atribuir qualquer _string_, não apenas o que está de acordo com a _realidade_, tal como fizemos acima. Isso expõe uma certa vulnerabilidade na programação e não torna os nossos caninos verdadeiramente autônomos.

Além disso, estamos aqui em um exemplo bem básico, onde utilizamos um simples _print_. E se quiséssemos que cada um tivesse um bloco de código único para a parte de `executa()`?

Enfim, poderíamos ficar um bom tempo criticando o código acima. Obviamente, ele não é a melhor implementação do mundo. Mas, aqui podemos introduzir um recurso da _Orientação a Objetos_, que é a _Abstração_.

Vamos direto para o código.

**Exemplo 1: Adapte o código anterior para uma versão com Orientação a Objetos, focando em Abstração**

Podemos começar criando a nossa classe Canidae, com seus atributos essenciais:

```cpp
class Canidae {
private:
    std::string nome;
    int idade;
};
```

Perceba que adicionamos o `private` ali. Em breve, explicaremos o porquê.

Agora, vamos colocar o nosso método `executa()`. A graça é que, ao declarar ele enquanto método abstrato, não precisaremos estruturar a parte interna da função.

```cpp
class Canidae {
private:
    std::string nome;
    int idade;
public:
    // Método puramente abstrato ou Virtual Puro
    virtual std::string executa() = 0;

    // Métodos Concretos
    std::string getNome(){
        return nome;
    }

    void setNome(std::string novoNome){
        nome = novoNome;
    }
};
```

Perceba que retiramos a variável `"std::string nome_acao"`. Não vamos precisar dela!

Para fins de fazer um código mais limpo, vamos colocar para a função retornar uma `std::string`.

Na definição, colocamos o termo `virtual` antes e igualamos o método a zero. É assim que definimos _um método puramente abstrato_ ou _virtual puro_.

Além disso, temos abaixo alguns exemplos de _métodos concretos_.

Agora, o que faremos com aquela definição abstrata?

Vambora:

```cpp
class Raposa : public Canidae {
  std::string executa() override { return "A RAPOSA ROUBA"; }
};

class Cachorro : public Canidae {
  std::string executa() override { return "O CACHORRO TOMA"; }
};

class Lobo : public Canidae {
  std::string executa() override { return "O LOBO PEDE"; }
};
```

O que fizemos de diferente? Aqui, não temos apenas declarações de variáveis/estruturas. Aqui, definimos classes novas, que seguem o mesmo "molde" da classe pai: Canidae. Aquela sintaxe nova de definição `"class Raposa/Cachorro/Lobo : public Canidae"` indica justamente isso.

No caso, **Raposa, Cachorro e Lobo** são classes independentes entre si, que possuem em comum todas as implementações, diferindo apenas na programação do método abstrato.

No caso, todos possuem os atributos `std::string nome;` e `int idade;`, além dos métodos. Porém, em `executa()`, temos uma abertura para implementações individuais no corpo desse método. Isso permite com que façamos diferentes retornos, tal como foi demonstrado acima.

Isso permite maior limpeza, independência e escalabilidade no código.

Como ficaria a nossa `main()`?

```cpp
int main() {
  Canidae *kyubi = new Raposa();
  Canidae *snoopy = new Cachorro();
  Canidae *pidao = new Lobo();

  std::cout << kyubi->executa() << std::endl;
  std::cout << snoopy->executa() << std::endl;
  std::cout << pidao->executa() << std::endl;

  return 0;
}
```

Nas nossas novas declarações, colocamos poteiros para `Canidae`, os quais atribuimos alocações das novas classes com implementações do método abstrato.

Depois, apenas realizamos o print do valor retornado pelo acesso do método `executa()` de cada um.

Compilando e rodando, temos como saída:

```
❯ ./main
A RAPOSA ROUBA
O CACHORRO TOMA
O LOBO PEDE
```

Chegamos em um resultado muito parecido com o anterior! Só que, dessa vez, de maneira muito mais limpa e elegante.

Talvez você ache um pouco complicado. Mas, acredite em mim, isso aqui só pode parecer complicado no começo. A verdadeira complicação aparece quando um projeto baseado na nossa primeira implementação com estruturas começa a crescer seguindo aquela lógica que fizemos.

Com o uso da abstração, temos a liberdade para criar métodos exclusivos da nossa classe.

**Exemplo 2: Crie pelo menos um método exclusivo para uma das novas classes**

É possível fazer o seguinte aqui:

```cpp
class Lobo : public Canidae {
public:
  std::string executa() override { return "O LOBO PEDE"; }
  std::string mimDe() { return "MIM DÊ PAPAI"; }
  std::string uivo() { return "AAAAAUUUUUUU"; }
};

int main() {
  Canidae *kyubi = new Raposa();
  Canidae *snoopy = new Cachorro();
  Lobo *pidao = new Lobo();

  std::cout << kyubi->executa() << std::endl;
  std::cout << snoopy->executa() << std::endl;

  std::cout << pidao->executa() << std::endl;
  std::cout << pidao->mimDe() << std::endl;
  std::cout << pidao->uivo() << std::endl;

  return 0;
}
```

Perceba que, para que não tenhamos erro de compilação, temos que tornar o método `executa()` público neste caso em específico.

Compilando e rodando, temos:

```
❯ ./main
A RAPOSA ROUBA
O CACHORRO TOMA
O LOBO PEDE
MIM DÊ PAPAI
AAAAAUUUUUUU
```

<img src="../OOP-Cpp/imagens/01_lobopidao.jpg" width=200>

Enfatizamos aqui que as implementações poderiam ser qualquer coisa, não necessariamente valores sendo retornados!

Em suma: a classe `Canidae` funciona como um template de implementação, isso melhora a permanência/mantimento de código e mudanças internas podem ser realizadas sem afetar a parte externa do todo.

A escolha a respeito do que iremos abstrair no código varia de implementação para implementação. Podemos ficar muito tempo aqui debatendo diferentes filosofias de vida, etc.

Entretanto, indo direto ao ponto, e sendo até um pouco repetitivos, indicamos seguir basicamente o que fizemos no exemplo anterior!

Vamos programar várias classes com características em comum, variando apenas em alguns métodos em específico? Seria bacana manter o mesmo nome para alguns métodos, mesmo que eles acabem variando na implementação?

É viável, simplesmente, arquitetar uma classe mãe/pai que será utilizada como template para as demais e determinar esses métodos como sendo abstratos.

## 1.5 Como criar uma boa interface (API) para sua classe

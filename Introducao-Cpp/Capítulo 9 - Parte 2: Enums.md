# Capítulo 9: Structs e Enums

Sejam bem-vindos ao capítulo 9 do nosso curso!

Aqui, faremos uma introdução aos tipos compostos **Structs** e **enums**. Ambos fornecem grande ajuda na estruturação de um programa robusto em **C++**, com o principal sendo o uso de **Structs**.

Sem mais delongas, vamos começar:

## 9.2 Enums

Imagine que você está participando de um projeto de jogo RPG. Sua função é fazer um simples sistema o qual imprime na tela o equipamento que, atualmente, está equipado por um jogador.

Existem cinco opções de equipamento: **espada, escudo, arco, cajado, livro**.

Como você estruturaria da maneira mais básica possível esse sistema?

Vamos desenvolver esse exemplo de maneira simples.

A utilização explícita de **números mágicos** está fora de cogitação, não é interessante nos basearmos em algo do tipo. Podemos definir, por exemplo, cada equipamento como uma constante e utilizar um **switch**.

**Exemplo 1: defina os equipamentos anteriormente mencionados como constantes e utilize um switch para imprimir qual está equipado (utilize uma variável chamada "equipado")**

Aqui, não tem muito segredo:

```cpp
#include <iostream>

//Definindo constantes
constexpr int espada = 0;
constexpr int escudo = 1;
constexpr int arco = 2;
constexpr int cajado = 3;
constexpr int livro = 4;

int main(){

    //Variável que representa o equipamento equipado
    int equipado = espada;

    //Estrutura de switch com os prints
    switch(equipado){
        case espada:
            std::cout << "Espada equipada!" << std::endl;
            break;
        case escudo:
            std::cout << "Escudo equipado!" << std::endl;
            break;
        case arco:
            std::cout << "Arco equipado!" << std::endl;
            break;
        case cajado:
            std::cout << "Cajado equipado!" << std::endl;
            break;
        case livro:
            std::cout << "Livro equipado!" << std::endl;
            break;
    }
}
```

Perceba que, no caso do switch, não poderíamos usar Strings com cases (por quê?).

Podemos, também, deixar o código um pouco mais legível da seguinte forma:

```cpp
#include <iostream>

//Podemos realizar a seguinte definição
using Equipamento = int;

//Definindo constantes com a nova definição Equipamento
constexpr Equipamento espada = 0;
constexpr Equipamento escudo = 1;
constexpr Equipamento arco = 2;
constexpr Equipamento cajado = 3;
constexpr Equipamento livro = 4;

int main(){

    //Variável que representa o equipamento equipado
    Equipamento equipado = espada;

    //Estrutura de switch com os prints
    switch(equipado){
        case espada:
            std::cout << "Espada equipada!" << std::endl;
            break;
        case escudo:
            std::cout << "Escudo equipado!" << std::endl;
            break;
        case arco:
            std::cout << "Arco equipado!" << std::endl;
            break;
        case cajado:
            std::cout << "Cajado equipado!" << std::endl;
            break;
        case livro:
            std::cout << "Livro equipado!" << std::endl;
            break;
    }
}
```

De fato, o que fizemos até aqui já possui um nível de organização mais adequado do que, por exemplo, o uso de alguns números mágicos. Porém, **Equipamento** ainda segue sendo um apelido para **int**. Ou seja, na prática, ainda podemos fazer algo do tipo:

```cpp
//Variável que representa o equipamento equipado
Equipamento equipado = 40028922; // (???)
```

Então, chega de mistério. Vamos reescrever o nosso código acima com o uso de **enums**.

De acordo com o [Capítulo 13.2](https://www.learncpp.com/cpp-tutorial/unscoped-enumerations/) do [Learn C++](https://www.learncpp.com),

**"Uma enumeração (também chamada de tipo enumerado ou enum) é um tipo de dado composto cujos valores são restritos a um conjunto de constantes simbólicas nomeadas (chamadas enumeradores)."**

A partir disso, acompanhe o exemplo:

**Exemplo 2: reescreva o código anterior utilizando enums**

Podemos, literalmente, manter todo o corpo da função **main** e reorganizar as definições anteriores.

Isso aqui:

```cpp
//Podemos realizar a seguinte definição
using Equipamento = int;

//Definindo constantes com a nova definição Equipamento
constexpr Equipamento espada = 0;
constexpr Equipamento escudo = 1;
constexpr Equipamento arco = 2;
constexpr Equipamento cajado = 3;
constexpr Equipamento livro = 4;
```

Pode ser convertido em:

```cpp
//Enumeração
enum Equipamento{
    //Enumeradores
    espada,
    escudo,
    arco,
    cajado,
    livro,
};
```

Que é um exemplo de sintaxe básica para definição de uma **enumeração**.

Quando definimos uma enumeração, cada enumerador é associado, de maneira automática, a um valor inteiro baseado na sua posição na lista de enumeradores. Por padrão, o primeiro enumerador é associado ao inteiro zero. Os outros enumeradores, sequencialmente, têm como valor associado o inteiro do anterior incrementado em 1. Logo,

```cpp
//Enumeração
enum Equipamento{
    //Enumeradores
    espada, // 0
    escudo, // 1
    arco,   // 2
    cajado, // 3
    livro,  // 4
};
```

Que, coincidentemente, são os mesmos valores que atribuímos a cada um na versão sem enum.

Claro, podemos também fazer associações diretas:

```cpp
//Enumeração
enum Equipamento{
    //Enumeradores
    espada = 4, // 4
    escudo,     // 5
    arco,       // 6
    cajado,     // 7
    livro,      // 8
};
```

Ou...

```cpp
//Enumeração
enum Equipamento{
    //Enumeradores
    espada = -3, // -3
    escudo,      // -2
    arco = 7,    // 7
    cajado = 7,  // 7
    livro,       // 8
};
```

Perceba que, no caso acima, atribuímos o mesmo inteiro ao **arco** e ao **cajado**. No caso, eles serão considerados a mesma coisa em eventuais implementações.

Enfim, vamos considerar o primeiro enum programado. Além disso, coloquemos um print na linha seguinte à declaração de **equipado**. A estruturação do nosso programa, então, ficou assim:

```cpp
#include <iostream>

enum Equipamento{
    //Enumeradores
    espada,     // 0
    escudo,     // 1
    arco,       // 2
    cajado,     // 3
    livro,      // 4
};

int main(){

    Equipamento equipado;
    std::cout << "Valor associado ao equipamento equipado: "<< equipado << std::endl;

    switch(equipado){
        case espada:
            std::cout << "Espada equipada!" << std::endl;
            break;
        case escudo:
            std::cout << "Escudo equipado!" << std::endl;
            break;
        case arco:
            std::cout << "Arco equipado!" << std::endl;
            break;
        case cajado:
            std::cout << "Cajado equipado!" << std::endl;
            break;
        case livro:
            std::cout << "Livro equipado!" << std::endl;
            break;

    }
    return 0;
}
```

Se compilarmos e rodarmos o programa acima, provavelmente será impresso um lixo de memória ou algo do tipo.

Quando fazemos a seguinte inicialização, teremos o valor zero sendo atribuído à nossa enumeração:

```cpp
Equipamento equipado{};// inicialização de valor inicializa para o valor 0
```

Isso ocorre mesmo se não tivermos um enumerador com aquele inteiro associado em nossa definição prévia. Portanto, uma boa prática é reservar o **inteiro zero** para o valor semântico mais "padrão" da sua enumeração. "Como assim?"

Pense no nosso exemplo do RPG. Por padrão, no que diz respeito ao equipamento do jogador, o que será que poderíamos associar ao número zero?

Exemplificadamente, podemos fazer o seguinte:

```cpp
enum Equipamento{
    //Enumeradores
    nenhum,     // 0
    espada,     // 1
    escudo,     // 2
    arco,       // 3
    cajado,     // 4
    livro,      // 5
};
```

Assim, ao adicionar o case para **nenhum**, nosso código fica desse jeito:

```cpp
#include <iostream>

enum Equipamento{
    //Enumeradores
    nenhum,     // 0
    espada,     // 1
    escudo,     // 2
    arco,       // 3
    cajado,     // 4
    livro,      // 5
};

int main(){

    Equipamento equipado{};
    std::cout << "Valor associado ao equipamento equipado: "<< equipado << std::endl;

    switch(equipado){
        case nenhum:
            std::cout << "Nenhum equipamento equipado!" << std::endl;
            break;
        case espada:
            std::cout << "Espada equipada!" << std::endl;
            break;
        case escudo:
            std::cout << "Escudo equipado!" << std::endl;
            break;
        case arco:
            std::cout << "Arco equipado!" << std::endl;
            break;
        case cajado:
            std::cout << "Cajado equipado!" << std::endl;
            break;
        case livro:
            std::cout << "Livro equipado!" << std::endl;
            break;

    }
    return 0;
}
```

Digamos, então, que seja do nosso interesse atribuir o **arco** ao **equipado**. Podemos fazer isso de algumas maneiras:

```cpp
Equipamento equipado = arco;
```

Ou...

```cpp
Equipamento equipado { arco };
```

Ou, utilizando **static_cast<type>()**:

```cpp
Equipamento equipado { static_cast<Equipamento>(3) };
```

pois, isso aqui não funcionaria:

```cpp
Equipamento equipado = 3; // Você terá um erro de compilação
```

Agora, com a ferramenta **enum**, você é capaz de organizar melhor sua codificação.

## Conclusões

Nesta segunda parte do Capítulo 9, você foi introduzido à utilização básica e enumerações em seu código na linguagem **C++**. Novamente, caso queira se aprofundar, recomendamos o [Learn C++](https://www.learncpp.com/), mais especificamente os Capítulos [13.1](https://www.learncpp.com/cpp-tutorial/introduction-to-program-defined-user-defined-types/), [13.2](https://www.learncpp.com/cpp-tutorial/unscoped-enumerations/), [13.3](https://www.learncpp.com/cpp-tutorial/unscoped-enumerator-integral-conversions/) e [13.4](https://www.learncpp.com/cpp-tutorial/converting-an-enumeration-to-and-from-a-string/), que foi onde nos inspiramos para formular esta explicação.

Aguardo você no próximo capítulo!

Até mais!

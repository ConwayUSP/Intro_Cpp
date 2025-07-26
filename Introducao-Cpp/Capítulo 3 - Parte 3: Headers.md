# Capítulo 3: Funções e Arquivos

Sejam bem-vindos ao Capítulo 3 do nosso curso!

Aqui, abordaremos, na linguagem C++, uma introdução ao uso de funções, programas com múltiplos arquivos e headers.

## 3.3 Introdução aos headers

Nas duas últimas partes deste capítulo, demonstramos o uso de funções, que faz parte essencial da estruturação de um projeto em C++. Além disso, o uso de vários arquivos para a composição do nosso programa também recebeu destaque. Ambos são fundamentais para a organização das partes de um programa e, com certeza, foi interessante sair de um código procedural escrito inteiramente na **main()** para algo levemente mais sofisticado.

Agora, vamos tratar a respeito dos headers.

Para nos livrarmos, por exemplo, da amarra de ter que sempre fazer as declarações das funções no arquivo onde a **main()** está presente, a introdução desse tipo de arquivo na organização do projeto é de suma importância.

Quando digitamos em qualquer arquivo **.cpp**, por exemplo,
```cpp
#include <iostream>
```
já estamos usufruindo dessa ferramenta.

O que acontece aqui é, basicamente, uma comunicação do programador com uma das etapas anteriores ao proceso de compilação, que é o trabalho do **pré-processador**: a fase de pré-processamento.

Quando fazemos **#include** de um arquivo, o pré-processador "substitui" a diretiva com os conteúdos presentes no arquivo. No caso, teremos os conteúdos presentes no arquivo **iostream**. Eles também serão pré-processados, assim como o que for necessário no resto do nosso projeto.

Ou seja, já estávamos utilizando headers deste o começo. Ora, vamos dar destaque aos pontos principais.

Caso você queira se aprofundar, recomendamos novamente o [Learn C++](https://www.learncpp.com/), mais especificamente a parte do [pré-processador](https://www.learncpp.com/cpp-tutorial/introduction-to-the-preprocessor/). Nos baseamos nesse capítulo para elaborar a explicação.

**Recapitulando...**

Anteriormente, organizamos o nosso pequeno exemplo de projeto na forma de três arquivos:

```
main.cpp
```
```cpp
#include <iostream>

int calculaFatorial(int num);
int maiorValor(int num1, int num2);
int entradaDeValores();

int main() {
    /*A seguir, chamamos a função duas vezes e atribuímos os valores retornados
    em duas variáveis diferentes*/
    int arg1 = entradaDeValores();
    int arg2 = entradaDeValores();
   //Aqui, printamos o fatorial do maior valor entre os dois:
    std::cout << "Fatorial do maior valor:" << calculaFatorial(maiorValor(arg1, arg2)) << "\n";
    return 0;
}
```

```
myFunctions.cpp
```
```cpp
int calculaFatorial(int num){
    //Caso base: se o nosso número for igual a 1 ou 0, retorne 1
    if(num == 1 || !num) return 1;
    //Se não cairmos no caso base, calculemos o fatorial normalmente, de forma recursiva:
    return num * calculaFatorial(num - 1);
}

int maiorValor(int num1, int num2){
    //O num1 é maior do que num2? Se sim, retorne num1. Caso contrário, retorne num2.
    return num1 > num2 ? num1 : num2;
}
```

```
myFunctions2.cpp
```
```cpp
#include <iostream>

int entradaDeValores(){
    int num;
    std::cout << "Digite um inteiro maior ou igual a zero: ";
    std::cin >> num;
    return num;
}
```

Sendo que os dois últimos, **myFunctions.cpp** e **myFunctions2.cpp**, eventualmente foram colocados em um único diretório separado chamado **functions**.

Para fins didáticos, vamos voltar a supor que os três estão no mesmo diretório.

Agora, criemos um novo arquivo, com a extensão **.h**, nesse mesmo diretório. Vamos chamar esse arquivo de **myFunctions.h**. Essa extensão diz respeito, justamente, a arquivos header.

Uma curiosidade é que não precisamos, necessariamente, utilizar o **.h** : eles podem aparecer, por exemplo, com **.hpp** ou, até mesmo, sem nenhuma extensão. Mas, para fins de boas práticas, aqui vamos seguir a convenção do **.h**.

**Exemplo 1: crie um header, com todas as funções declaradas anteriormente, para o nosso pequeno projeto**

No nosso novo arquivo, vamos fazer as declarações das funções presentes em **myFunctions.cpp** e **myFunctions2.cpp**. E, então, removemos as declarações realizadas na função **main()**.

```
myFunctions.h
```
```cpp
//(Caso você já conheça os header guards, calma...)
int calculaFatorial(int num);
int maiorValor(int num1, int num2);
int entradaDeValores();
```
Aliás, uma "boa prática" a ser considerada na hora de criar arquivos header é, justamente, nomeá-lo com o mesmo nome utilizado pelo arquivo onde as definições das funções estão presentes.
Neste caso, para fins didáticos, estamos com dois arquivos **.cpp**. Porém, é nítido que eles poderiam ser apenas um **myFunctions.cpp**.
```
main.cpp
```
```cpp
#include <iostream>

int main() {
    int arg1 = entradaDeValores();
    int arg2 = entradaDeValores();
    std::cout << "Fatorial do maior valor: " << calculaFatorial(maiorValor(arg1, arg2)) << "\n";
    return 0;
}
```

É claro que, se tentarmos compilar o projeto após essas alterações, não iremos conseguir (por quê?).

Como faremos para "ligar" o nosso arquivo **main.cpp** às funções anteriormente implementadas? Observe:

```
main.cpp
```
```cpp
#include <iostream>
/*Vamos incluir o nosso novo arquivo header */
#include "myFunctions.h"

int main() {
    int arg1 = entradaDeValores();
    int arg2 = entradaDeValores();
    std::cout << "Fatorial do maior valor: " << calculaFatorial(maiorValor(arg1, arg2)) << "\n";
    return 0;
}
```

```
myFunctions.cpp
```
```cpp
/*Vamos incluir o nosso novo arquivo header */
#include "myFunctions.h"

int calculaFatorial(int num){
    //Caso base: se o nosso número for igual a 1 ou 0, retorne 1
    if(num == 1 || !num) return 1;
    //Se não cairmos no caso base, calculemos o fatorial normalmente, de forma recursiva:
    return num * calculaFatorial(num - 1);
}

int maiorValor(int num1, int num2){
    //O num1 é maior do que num2? Se sim, retorne num1. Caso contrário, retorne num2.
    return num1 > num2 ? num1 : num2;
}
```

```
myFunctions2.cpp
```
```cpp
#include <iostream>
/*Vamos incluir o nosso novo arquivo header */
#include "myFunctions.h"

int entradaDeValores(){
    int num;
    std::cout << "Digite um inteiro maior ou igual a zero: ";
    std::cin >> num;
    return num;
}
```

E, agora, vamos compilar:
```
g++ *.cpp -o nomeDoArquivo
```

Se tudo estiver correto, devemos obter o mesmo resultado da versão anterior do nosso projeto.

Algumas coisas são importantes a serem destacadas sobre o que fizemos acima:

**(1) Perceba a diferença entre o #include de iostream e o de myFunctions.h:**
```cpp
#include <iostream> //Aqui, utilizamos <>
#include "myFunctions.h" //Aqui, utilizamos ""
```
Para incluir arquivos inerentes ao sistema ou ao compilador, usamos <>;
Para incluir os novos arquivos que criamos, usamos "".


**(2) É uma boa prática realizar o include do header em todos os arquivos nos quais definimos nossas funções**

Caso queira remover o include dos arquivos **myFunctions.cpp** e **myFunctions2.cpp**, fique à vontade. Você ainda conseguirá compilar utilizando o mesmo comando.

Porém, de acordo com o capítulo sobre [Arquivos Header](https://www.learncpp.com/cpp-tutorial/header-files/), do [Learn C++](https://www.learncpp.com/),

"In C++, it is a best practice for code files to #include their paired header file (if one exists). This allows the compiler to catch certain kinds of errors at compile time instead of link time."

"Em C++, é uma prática recomendada que os arquivos de código incluam o arquivo de cabeçalho correspondente (se houver). Isso permite que o compilador detecte certos tipos de erros em tempo de compilação, em vez de no momento de link."

**(3) Quando uma header é incluído, os headers incluídos nele também são**

Experimente, nosso projeto de exemplo, remover a **iostream** do **main.cpp** e declarar ela no **myFunctions.h**. Como a inclusão do myFunctions.h foi mantida, a **iostream** também será incluída recursivamente. O código poderá ser compilado sem problemas. Chamamos esse tipo de inclusão de "transitive includes" (inclusões transitivas).

Não é positivo se apoiar nesse tipo de inclusão. Na realidade, é uma boa prática fazer com que todos os arquivos tenham inclusões explícitas dos headers necessários para seu funcionamento. Fica como exercício para o leitor a elaboração de uma justificativa para tal.

**Para essas e outras informações mais detalhadas, visite o capítulo sobre [Arquivos Header](https://www.learncpp.com/cpp-tutorial/header-files/), do [Learn C++](https://www.learncpp.com/).**

Agora, e se quisermos incluir headers advindos de algum outro diretório?

**Exemplo 2: mova os arquivos myFunctions.h, myFunctions.cpp e myFunctions2.cpp de volta para o diretório functions anteriormente utilizado e faça o #include de maneira correta no arquivo main()**

Para isso, após movermos os arquivos, podemos simplesmente incluir o caminho relativo até o header:

```cpp
#include <iostream>
//Alteramos aqui, para utilizar o caminho relativo
#include "functions/myFunctions.h"


int main() {
    int arg1 = entradaDeValores();
    int arg2 = entradaDeValores();
    std::cout << "Fatorial do maior valor: " << calculaFatorial(maiorValor(arg1, arg2)) << "\n";
}
```

Porém, um jeito melhor de fazer isso pode ser comunicar ao seu compilador ou à sua IDE a presença dos headers em outro diretório.

## Conclusões

Nesta terceira parte do Capítulo 3, você teve um primeiro contato com programação em C++ utilizando arquivos header.

Não deixe de conferir os próximos capítulos! Até mais!

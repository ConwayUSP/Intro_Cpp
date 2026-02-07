# Capítulo 8 - Referências e Ponteiros

Sejam bem-vindos ao Capítulo 8 do nosso curso!

Aqui, trabalharemos pela primeira vez de maneira diretamente orientada a endereços em memória, o que geralmente é bem importante para a estruturação de um programa mais complexo.

Ponteiros são conhecidos por serem o terror da programação em linguagens de nível mais baixo. Porém, veremos a seguir que não é nada extraordinariamente difícil, apesar de ser necessária uma revisão de vez em quando.

## O operador "Endereço de" (&)

Quando declaramos uma variável, atribuindo ou não um valor, um pedaço da memória RAM será associado a ela. Provavelmente, eventualmente o nosso programa vai interagir de alguma maneira com aquela variável. Quando isso acontece, o programa tentará, justamente, acessar o endereço dela para recuperar, alterar, etc, a informação ali presente.

Mesmo que os endereços de memória não sejam expostos por padrão para o programador, nós podemos ter acesso a essa informação de maneira bem direta na linguagem C++ através do operador "&". Observe:

```cpp
#include <iostream>

int main(){
    
    int x = 7;
    
    std::cout << x << '\n'; //Printando o valor atribuído à variável x
    std::cout << &x << '\n'; // Printando o endereço em memória da variável x
    
    return 0;
}

```

Como sempre: compile e rode o código em sua máquina.

No computador do autor deste capítulo, tivemos o seguinte resultado no terminal:

```
7
0x7ffc8ab85e04
```

Sequencialmente, nós utilizamos o operador "&" para recuperar o endeço de "x" e, em seguida, imprimir. 
No caso, endereços de memória são tipicamente printados na forma de valores em hexadecimal.


## O operador de "desreferência" (*)

Agora, e se eu tiver um endereço de memória e quiser acessar o valor ali presente? Simplesmente, o operador "*" retorna o valor de um dado endereço. Perceba:

```cpp
#include <iostream>

int main(){
    
    int x = 7;
    
    std::cout << x << '\n'; //Printando o valor atribuído à variável x
    std::cout << &x << '\n'; // Printando o endereço em memória da variável x
    
    std::cout << *(&x) << '\n'; // Printando o valor no endereço de memória da variável x
    
    return 0;
}

```

Aqui, tivemos como resultado:

```
7
0x7fff3c7fdc94
7
```

Inclusive, é possível notar que, comparando o endereço deste exemplo com o do anterior, ocorreu uma diferença. Obviamente, endereços são voláteis e podem ser alterados em cada execução do programa. (Por quê?)

Neste exemplo, o fato de chegarmos novamente no valor 7 é um bom sinal (você poderia levar sua máquina para o exorcista, se isso não acontecesse). Basicamente, utilizamos o "*" para recuperarmos o valor ali "guardado" naquele endereço e printamos no terminal.

Isso pareceu, talvez, um pouco inútil caso você nunca tenha tido contato com esse tipo de coisa. Mas, com esses dois operadores "&" e "*", podemos começar a falar sobre ponteiros.


## Ponteiros

Basicamente, um ponteiro é um objeto no qual armazenamos endereços de memória enquanto seu valor. Normalmente, armazenamos de outras variáveis/objetos para usarmos depois.

Um tipo que especifica um ponteiro é denominado _tipo ponteiro_. Referências de tipos são declaradas utilizando "&", enquanto Ponteiros de tipos são declarados utilizando "*":

```cpp
int;  // Um inteiro normal
int&; // Uma referência para um valor inteiro
int*; // Um ponteiro para um valor inteiro (guarda o endereço de um valor inteiro)
```

Perceba que, ao declarar um ponteiro, precisamos especificar o tipo de dado que ele irá apontar. Por exemplo, se quisermos criar um ponteiro para um inteiro, precisamos declará-lo como `int*`, se quisermos criar um para um _float_, precisamos declará-lo como `float*`, etc.

Além disso, note que, neste caso, o asterísco é parte da sintaxe de declaração para ponteiros, não o uso do operador de desreferência.

Para declarar múltiplos ponteiros em uma única linha, lembre de incluir o asterísco para cada variável:

```cpp
int* ptr1, * ptr2; // Um ponteiro para um valor inteiro (guarda o endereço de um valor inteiro)
```

Tipicamente, ponteiros são usados para guardar o endereço de alguma outra variável (que pegamos ao utilizar o operador '&'). Uma vez que tenhamos um ponteiro apontando para outro objeto, podemos usar o operador de desreferência '*' para recuperar o valor naquele endereço. A sintaxe pode causar um pouco de confusão no começo, mas é razoaveelmente simples:

```cpp
#include <iostream>

int main(){
    
    int x{ 7 };
    std::cout << x << '\n'; // pritando valor de x
    int* ptr{ &x }; // ptr guarda endereço de x
    std::cout << ptr << '\n'; // Printando o endereço de x
    std::cout << *ptr << '\n'; // Printando o valor atribuído à variável x

    return 0;
}
```

Compilando e rodando o código acima, teremos:

```
7
0x7fff6d6b489c
7
```

Maravilha. Agora, preste atenção no código abaixo:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int* ptr{ &x }; 

    std::cout << x << '\n';    
    std::cout << *ptr << '\n'; 

    *ptr = 6; 

    std::cout << x << '\n';
    std::cout << *ptr << '\n'; 

    return 0;
}
```

Ele imprime no terminal:
```
5
5
6
6
```

Por quê?

Repare no que acontece em
```cpp
*ptr = 6; 
```

O que ocorre aqui é que desreferenciamos o objeto apontado por _ptr_, o que possibilita que façamos a atribuição do valor 6 a ele. A variável "original" (x), ora, tem seu valor alterado justamente por realizarmos essa operação através do ponteiro.

Prosseguindo, é válido ressaltar, também, que o operador "Endereço de" (&) retorna, justamente, um ponteiro, não o endereço de seu operando na forma de literal. Além disso, o tamanho em memória de um ponteiro depende da arquitetura onde ocorreu a compilação do executável, que dita o tamanho em bits dos endereços de memória.

Por fim, falando brevemente sobre os _dangling pointers_, ou ponteiros pendentes/pendurados: 

Basicamente, um _dangling pointer_ é um ponteiro que guarda o endereço de um objeto o qual não é mais válido. Desreferenciar um _dangling pointer_ fomentará um comportamento indefinido do nosso programa, visto que você está tentando acessar um objeto inválido.

# Conclusões

Agora, você possui uma noção básica a respeito dos dois operadores os quais são utilizados para interagir com endereços, além do próprio conceito de ponteiros.

Na próxima parte, falaremos sobre ponteiros nulos e inteligentes. Vejo você lá!

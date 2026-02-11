# Capítulo 01 - Parte 2: Introdução à biblioteca "iostream"

Nesta parte, falaremos mais sobre `std::cout`, que usamos em nosso programa Hello world! para enviar o texto "*Hello world!*" para o console (programa de interface que possui comandos para imprimir e ler texto). 

Também exploraremos como obter informações do usuário, o que usaremos para tornar nossos programas mais interativos.

## 1.5 A Biblioteca "iostream" 

A biblioteca `<iostream>` permite interação básica com o usuário. 

Usaremos a funcionalidade desta biblioteca para obter a entrada do teclado e enviar dados para o console. A parte 'io' de iostream significa entrada/saída .

Como utilizar a funcionalidade definida na biblioteca iostream:

```cpp
#include <iostream>

// resto do código que utiliza a funcionalidade dessa biblioteca
```

### I) `std::cout` (Para saída de dados)

A biblioteca iostream contém algumas variáveis ​​predefinidas para usarmos. 

Uma das mais úteis é `std::cout` , que nos permite enviar dados ao console para serem impressos como texto. 'cout' significa "saída de caracteres".

Retomando o nosso programa *Hello, world!*: 

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, world!";     // Imprimi Hello, world! na tela
    return 0;
}
```

Dentro da nossa função principal, usamos `std::cout`, juntamente com o **operador de inserção ( << )** , para enviar o texto "Olá, mundo!" para o console para ser impresso.

Para imprimir mais de um item na mesma linha, o operador de inserção ( << ) pode ser usado várias vezes em uma única instrução para concatenar várias partes da saída. Por exemplo:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello," << " world!";  
    return 0;
}
```

### II) `std::cin` (Para entrada de dados)

`std::cin` é outra variável predefinida na biblioteca iostream. Enquanto `std::cout` imprime dados no console (usando o operador de inserção << para fornecer os dados), `std::cin` (que significa "entrada de caracteres") lê a entrada do teclado.

Normalmente, usamos o **operador de extração ( >> )** para inserir os dados de entrada em uma variável (que pode então ser usada em instruções subsequentes).

```cpp
#include <iostream>

int main() {

    int idadeUsuario;
    std::cout << "Qual sua idade? ";      // Imprimi Qual sua idade?
    std::cin  >> idadeUsuario;            // Captura a entrada do teclado
    return 0;
}
```

Outro exemplo:

```cpp
#include <iostream>  

int main()
{
    std::cout << "Digite dois números separados por espaço: ";

    int x, y;

    std::cin >> x >> y;                  // Pega os dois números e guarda nas variáveis x e y respectivamente

    std::cout << "Você digitou " << x << " e " << y << '\n';

    return 0;
}
```
## Questões complementares

1) Dê um exemplo de código que imprime:
```cpp
A soma de 3 e 5 é 8
```

2) Escreva um programa que:
- Pergunte ao usuário o seu nome.
- Pergunte a idade.
- Mostre uma mensagem: `"Olá <nome>, você tem <idade> anos!".`
  
3) Crie um programa em C++ que:
- Pergunte ao usuário seu nome e idade.
- Pergunte quantos anos ele quer avançar no tempo.
- Calcule e mostre a idade que ele terá no futuro usando a frase:

```cpp
Olá <nome>, daqui a <anosFuturos> anos você terá <novaIdade> anos!
```
## Conclusões

Neste capítulo, aprendemos sobre o uso e a importância da biblioteca `<iostream>` para deixar os nossos programas mais interativos por meio do uso de `std::cout` (para saída de dados) e `std::cin` (para entrada de dados).

Te espero no próximo capítulo! :)

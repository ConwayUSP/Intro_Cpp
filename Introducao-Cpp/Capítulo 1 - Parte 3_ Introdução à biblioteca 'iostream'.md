# Capítulo 1 - Parte 3: Introdução à biblioteca "iostream"

Nesta parte, falaremos mais sobre `std::cout`, que usamos em nosso programa Hello world! para enviar o texto *Hello world!* para o console (programa de interface que possui comandos para imprimir e ler texto). 

Também exploraremos como obter informações do usuário, o que usaremos para tornar nossos programas mais interativos.

## 3.1 A Biblioteca "iostream" 

A biblioteca `<iostream>` permite interação básica com o usuário. 

Usaremos a funcionalidade desta biblioteca para obter a entrada do teclado e enviar dados para o console. A parte 'io' de iostream significa entrada/saída .

Para usar a funcionalidade definida na biblioteca iostream, precisamos incluir o cabeçalho iostream no topo de qualquer arquivo de código que use o conteúdo definido em iostream, assim:

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

`std::cout` pode também imprimir números e valores de variáveis.

Para imprimir mais de um item na mesma linha, o operador de inserção ( << ) pode ser usado várias vezes em uma única instrução para concatenar várias partes da saída. Por exemplo:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello," << " world!";  
    return 0;
}
```
Saída esperada:
```
Hello, world!
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
Saída esperada:
```
Qual sua idade? --        (-- é o número dado pelo usuário)
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
Saída esperada:
```
Digite dois números separados por espaço: -- --         //(-- é o número dado pelo usuário)
Você digitou -- e --
```

### III) `\n` (Quebra de linha)

Se quisermos imprimir linhas separadas de saída no console, precisamos instruí-lo a mover o cursor para a próxima linha. Podemos fazer isso imprimindo uma nova linha. 

Uma maneira de gerar uma nova linha é escrever '\n' (que significa “fim de linha”):
```cpp
#include <iostream> 

int main(){
    int x = 5;
    std::cout << "x é igual a: " << x << '\n';           // entre aspas simples (convencional)
    std::cout << "Sim." << "\n";                         // entre aspas duplas (não convencional, mas aceitável)
    std::cout << "Conway melhor entidade de SI?!\n";     // entre aspas duplas no texto existente (convencional)
    return 0;
}
```
Saída esperada:
```
x é igual a: 5
Sim.
Conway melhor entidade de SI?!
```
## Conclusões

Neste capítulo, aprendemos sobre o uso e a importância da biblioteca `<iostream>` para deixar os nossos programas mais interativos por meio do uso de `std::cout` (para saída de dados) e `std::cin` (para entrada de dados).

Além disso, vimos o uso do `\n` para pular para próxima linha e o código ficar com uma aparência mais agradável.

Te espero no próximo capítulo! :)


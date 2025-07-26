# Capítulo 3: Funções e Arquivos

Sejam bem-vindos ao Capítulo 3 do nosso curso!

Aqui, abordaremos, na linguagem C++, uma introdução ao uso de funções, programas com múltiplos arquivos e headers.

## 3.2 Introdução a programas com múltiplos arquivos

Na primeira parte, aproveitamos o tópico de funções para tocar um pouco em conceitos mais básicos referentes à organização estrutural do nosso código. Por exemplo, o simples uso de declarações de cabeçalhos em nossa codificação de funções já é fator relevante à criação de um código legível.

**Recapitulando...**

Esse foi o código resultante do nosso último capítulo:

```cpp
#include <iostream>

int calculaFatorial(int num);
int maiorValor(int num1, int num2);

int main() {
    std::cout << calculaFatorial(maiorValor(7, 3)) << "\n"; //Aqui, printamos o fatorial do maior valor entre 7 e 3
    return 0;
}

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

Agora, podemos dar mais um passo: e se quiséssemos separar a estrutura do nosso programa em múltiplos arquivos?

Isso não só é possível como, também, é altamente necessário para projetos maiores.

Vamos começar com algo mais simplificado.
Uma maneira de realizar essa separação reside, simplesmente, na criação de um arquivo **.cpp** paralelo, com as funções desejadas. No caso, manteremos a declaração das funções no nosso arquivo inicial, o qual contará com a função **main()**. E, por fim, compilaremos o nosso projeto.

**Exemplo 1: realize a divisão do programa inicial representado acima em dois arquivos diferentes**

Podemos estruturar o projeto da seguinte maneira, no mesmo diretório:

Manteremos a nossa função **main()** e a declaração das outras duas funções anteriormente implementadas em um único arquivo chamado **main.cpp**
```
main.cpp
```
```cpp
#include <iostream>

int calculaFatorial(int num);
int maiorValor(int num1, int num2);

int main() {
    std::cout << calculaFatorial(maiorValor(7, 3)) << "\n"; //Aqui, printamos o fatorial do maior valor entre 7 e 3
    return 0;
}
```

Criaremos um outro arquivo **.cpp**. Neste exemplo, vamos utilizar o nome genérico **myFunctions.cpp**. Ele conterá as funções que implementamos anteriomente, com mesmo cabeçalho declarado no arquivo **main.cpp**

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

Então, vamos compilar. A diferença é que faremos isso para os dois arquivos:

```
g++ main.cpp myFunctions.cpp -o nomeDoArquivoExecutavel
```

A ordem dos arquivos a serem compilados não importa, contanto que estejam no espaço adequado para compilação, isto é, os arquivos a serem compilados devem estar agrupados em posição específica (que foi explicada anteriormente no curso) para que o compilador entenda corretamente como realizar o trabalho.

Assim, como apenas temos o mesmo programa, só que dividido em dois arquivos, não haverá diferença na execução (se tudo estiver correto).

Podemos criar quantos arquivos quisermos, contanto que as condições de organização acima sejam respeitadas. Depois, basta compilar os arquivos em um único executável.

Vale ressaltar que, como as funções **calculaFatorial** e **maiorValor** não utilizam funcionalidades de alguma biblioteca incluída, podemos simplesmente jogar elas no arquivo separado e realizar a compilação. Porém, caso utilizássemos algo inerente a uma biblioteca em específico, teríamos que realizar o **#include** no arquivo distinto com as funções.

**Exemplo 2: crie, em um terceiro arquivo .cpp, uma função que peça para que o usuário digite um número inteiro maior ou igual a zero e que retorne esse valor. Faça uma declaração dessa nova função no arquivo principal e um exemplo de aplicação na main(). Você pode assumir que o usuário sempre irá passar números inteiros maiores ou iguais a zero.**

Vamos começar criando o novo arquivo **.cpp**. O nome dele será **myFunctions2.cpp**. Além disso, como utilizaremos mecanismos de entrada/saída, vamos incluir a **iostream**. O nome da nova função será, para este exemplo, **entradaDeValores**. Assim, o corpo da nossa função será:

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

Ora, em nosso **main.cpp**, vamos fazer a declaração e um exemplo de aplicação:

```
main.cpp
```
```cpp
#include <iostream>

int calculaFatorial(int num);
int maiorValor(int num1, int num2);
int entradaDeValores(); //Declaração

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

Logo, vamos compilar.

Podemos fazer deste jeito:

```
g++ main.cpp myFunctions.cpp myFunctions2.cpp -o nomeDoArquivoExecutavel
```

Ou, se todos os **.cpp** presentes no diretório atual forem unicamente do nosso projeto, deste:

```
g++ *.cpp -o nomeDoArquivoExecutavel
```

Faça a implementação e compilação, e veja o resultado.

Vale mencionar que podemos, também, separar os arquivos em diferentes diretórios. Vamos lá:

**Exemplo 3: crie um novo diretório, dentro do local onde está o seu projeto, coloque os arquivos myFunctions.cpp e myFunctions2.cpp nele e compile o projeto novamente.**

Para este exemplo, vamos criar um diretório chamado **functions**. Depois de mover os arquivos, vamos compilar.

Para compilar, em terminal linux, basta digitar o caminho até o arquivo. Podemos fazer deste jeito:

```
g++ main.cpp ./functions/myFunctions.cpp ./functions/myFunctions2.cpp -o nomeDoArquivoExecutavel
```

O que é plenamente plausível e funcional. Porém, lembre-se que existe uma forma de compilar **todos** os **.cpp** dentro de um diretório:

```
g++ main.cpp ./functions/*.cpp -o nomeDoArquivoExecutavel
```

O resultado deverá ser o mesmo da compilação do Exemplo 2.


## Conclusões

Nesta segunda parte do Capítulo 3, você teve um primeiro contato com programação em C++ com múltiplos arquivos.

Vejo você na próxima parte! Até mais!

# Capítulo 3: Funções e Arquivos

Sejam bem-vindos ao Capítulo 3 do nosso curso!

Aqui, abordaremos, na linguagem C++, uma introdução ao uso de funções, programas com múltiplos arquivos e headers.

## 3.1 Introdução às Funções

Neste ponto, é válido mencionar mais uma maneira de descrever o que uma função diz respeito. No capítulo 2.1 do curso básico de C++, do site [Learn C++](https://www.learncpp.com), temos a seguinte descrição:

**"A function is a reusable sequence of statements designed to do a particular job."**

**"Uma função é uma sequência reutilizável de estados designados para realizar uma tarefa específica"**

De fato, você já entendeu que todo código nessa linguagem precisa de uma função chamada **main()**. Porém, para que o programa consiga ser extendido de maneira mais adequada, sem que coloquemos todas as linhas nela, podemos utilizar funções.

Aqui, temos o nosso exemplo de estrutura genérica de um programa, que só possui a função **main()**:
```cpp
#include <iostream>

int main() {
    // Aqui vai o código do programa
    return 0;
}
```
Como mencionado em capítulos anteriores, a função **main()** pode receber argumentos e retornar valores. No nosso exemplo, ela não recebe nenhum argumento (dentro do par de parênteses normais) e tem como valores retornados apenas inteiros (**int main()**), retornando, por padrão, o número zero (**return 0**).

As funções em C++, de modo geral, compartilham as mesmas características: recebem argumentos (inputs) e retornam um tipo de valor (outputs).

Como as linhas de código são executadas sequencialmente, quando a execução alcança a linha a qual possui uma chamada de função (é assim que, geralmente, nomeamos a "ativação" de uma função), salvamos o ponto onde estamos na realização das tarefas programadas do corpo de nossa função em questão, que pode ser a **main** ou qualquer outra que faça a chamada dela mesma (denominada **chamada recursiva**) ou de outra função.

Depois, nos deslocamos para o corpo da função a qual foi chamada e realizamos sequencialmente a execução de suas linhas de código.

Por fim, quando realizamos o retorno daquela função em questão, voltamos para o ponto onde paramos no corpo da "função de partida"

**Exemplo 1: faça uma função que receba como parâmetro um número inteiro positivo, calcule e retorne o seu fatorial**


Inicialmente, vamos começar a criar o corpo da nossa nova função:

```cpp
#include <iostream>

//Corpo
int calculaFatorial(int num){

}

int main() {
    // Aqui vai o código do programa
    return 0;
}
```

Temos, então, o começo da estrutura. Ora, colocamos ela acima da nossa **int main()**. Porém, para que nossa função principal não comece, com a inserção de mais e mais funções, a ficar isolada no final da nossa codificação, podemos utilizar os **cabeçalhos**. Observe:

```cpp
#include <iostream>

//Cabeçalho
int calculaFatorial(int num);

int main() {
    // Aqui vai o código do programa
    return 0;
}

//Corpo
int calculaFatorial(int num){

}
```

Ou seja, fazemos uma declaração acima da função main com as principais informações sobre nossa função **int calculaFatorial(int num)**: o nome e os tipos de valores recebidos e retornados. Porém, apenas implementamos ela, com seu corpo, depois da função principal.

Sobre a implementação em si: o fatorial de um número n, representado na matemática por n!, diz respeito a **n! = n.(n-1).(n-2).(...).1**, lembrando que 1! = 1 e 0! = 1.

Podemos implementar a mesma lógica estruturando o nosso raciocínio da seguinte maneira:

```cpp
int calculaFatorial(int num){
    if(num == 1 || !num) return 1; //Caso base: se o nosso número for igual a 1 ou 0, retorne 1
    return num * calculaFatorial(num - 1); //Se não cairmos no caso base, calculemos o fatorial normalmente, de forma recursiva
}
```

Temos, então, um exemplo clássico de função recursiva. Perceba que, apesar de supostamente simples, ela demonstra detalhes muito interessantes. A chamada recursiva ocorre, por exemplo, na mesma linha a qual ocorre o retorno. Note que existe uma "fila" de prioridade na realização de operações e instruções padronizadas.

O corpo do nosso programa, então, fica assim:

```cpp
#include <iostream>

int calculaFatorial(int num);

int main() {
    // Aqui vai o código do programa
    return 0;
}

int calculaFatorial(int num){
    if(num == 1 || !num) return 1; //Caso base: se o nosso número for igual a 1 ou 0, retorne 1
    return num * calculaFatorial(num - 1); //Se não cairmos no caso base, calculemos o fatorial normalmente, de forma recursiva
}
```

E, podemos chamar a função **calculaFatorial (int num)** na main para calcular o fatorial de um número:

```cpp
#include <iostream>

int calculaFatorial(int num);

int main() {
    std::cout << calculaFatorial(7) << "\n"; //Aqui, calculamos e printamos o fatorial do número 7.
    int fatorialDeDez = calculaFatorial(10); //Aqui, calculamos e atribuímos o valor retornado na variável "fatorialDeDez"
    return 0;
}

int calculaFatorial(int num){
    if(num == 1 || !num) return 1; //Caso base: se o nosso número for igual a 1 ou 0, retorne 1
    return num * calculaFatorial(num - 1); //Se não cairmos no caso base, calculemos o fatorial normalmente, de forma recursiva
}
```

**Exemplo 2: faça uma função que receba como argumento dois valores inteiros e retorne o maior entre eles**

Vamos começar, diretamente, com o cabeçalho:

```cpp
#include <iostream>

int calculaFatorial(int num);
int maiorValor(int num1, int num2);

int main() {
    std::cout << calculaFatorial(7) << "\n"; //Aqui, calculamos e printamos o fatorial do número 7.
    int fatorialDeDez = calculaFatorial(10); //Aqui, calculamos e atribuímos o valor retornado na variável "fatorialDeDez"
    return 0;
}

int calculaFatorial(int num){
    if(num == 1 || !num) return 1; //Caso base: se o nosso número for igual a 1 ou 0, retorne 1
    return num * calculaFatorial(num - 1); //Se não cairmos no caso base, calculemos o fatorial normalmente, de forma recursiva
}

int maiorValor(int num1, int num2){

}
```

Então, vamos implementar a nossa lógica utilizando **operador ternário**:

```cpp
int maiorValor(int num1, int num2){
    return num1 > num2 ? num1 : num2; //O num1 é maior do que num2? Se sim, retorne num1. Caso contrário, retorne num2.
}
```

Assim, podemos fazer uma implementação desse tipo na **main()**:

```cpp
#include <iostream>

int calculaFatorial(int num);
int maiorValor(int num1, int num2);

int main() {
    std::cout << calculaFatorial(maiorValor(7, 3)) << "\n"; //Aqui, printamos o fatorial do maior valor entre 7 e 3
    return 0;
}

int calculaFatorial(int num){
    if(num == 1 || !num) return 1; //Caso base: se o nosso número for igual a 1 ou 0, retorne 1
    return num * calculaFatorial(num - 1); //Se não cairmos no caso base, calculemos o fatorial normalmente, de forma recursiva
}

int maiorValor(int num1, int num2){
    return num1 > num2 ? num1 : num2; //O num1 é maior do que num2? Se sim, retorne num1. Caso contrário, retorne num2.
}
```

Repare que, analisando separadamente da realização de instruções, podemos nos basear diretamente nos valores retornados por elas.
Nitidamente, não temos que sempre estruturar uma função pensando unicamente em seu retorno. Para isso, geralmente utilizamos as funções **void**, onde não precisamos retornar um valor.

Fica, como dever de casa, então, a implementação de mais uma função, que seja **void**, para essa estrutura de programa a qual desenvolvemos neste capítulo! Use sua criatividade.

Agora, você possui uma noção melhor a respeito do uso e da estruturação mais básica de funções em C++!

Não deixe de ver a próxima parte! Até breve!

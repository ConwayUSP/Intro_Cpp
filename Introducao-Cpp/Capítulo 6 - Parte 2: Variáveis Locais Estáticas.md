# Capítulo 6: Namespaces e variáveis locais estáticas

Sejam bem-vindos ao Capítulo 6 do nosso curso!

Quando falamos de organização de código, existem muitas ferramentas capazes de auxiliar a estruturação dele. Neste capítulo, abordaremos mais alguns pontos importantes para a criação de programas mais robustos. Começando por **namespaces**, definidos pelo programador. Em seguida, abordaremos um pouco a respeito de **Static**, no contexto de variáveis locais.

## 6.2 Variáveis locais estáticas:

Para começar, vamos partir diretamente para um exemplo:

**Exemplo 1: implemente uma função recursiva e, após sua execução, faça com que o programa imprima na tela a quantidade de chamadas recursivas realizadas**

Uma abordagem válida para este cenário é a criação de uma variável global no nosso arquivo. Ela será incrementada conforme as chamadas forem ocorrendo.
Para este exemplo, qualquer implementação recursiva é válida. Vamos nos basear em uma implementada anteriormente no curso:

```cpp
#include <iostream>

/*Variável global, que será utilizada para
a contagem de chamadas recursivas*/
int counter = 0;

/*Novamente, a implementação da função recursiva
para cálculo de fatorial*/
int fatorial(int num){
    counter++;
    if(!num || num == 1) return 1;
    return num * fatorial(num - 1);
}

int main(){

    int numero;
    std::cout << "Insira um inteiro: ";
    std::cin >> numero;
    int fatorialNumero = fatorial(numero);

    /*Imprimindo */
    std::cout << "O número de chamadas recursivas foi: " << counter << "\n";
    std::cout << "O fatorial desse número é: " << fatorialNumero << "\n";
    return 0;
}
```

Nitidamente, tudo bem caso você tenha pensado em alguma outra maneira de realizar a contagem. Faça a compilação e rode o programa.

Agora, uma outra abordagem é, justamente, com o uso de **variáveis locais estáticas**.

Podemos declarar uma da seguinte maneira:

```cpp
static tipoDaVariavel variavel
```

Quando fazemos isso, alteramos a duração "normal" da variável local para a duração **estática**. A partir disso, a variável é criada no começo do programa e destruída somente no fim da execução dele. Isso difere da duração **automática** das variáveis locais, pois agora temos a permanência da variável após a eventual alteração de escopo, isto é, após a saída de um espaço definido por um par de chaves {}, por exemplo.

Observe:

```cpp
#include <iostream>

void printMensagem(){
    int num = 0;
    std::cout << "Número de vezes que printMensagem foi chamada: " << ++num << "\n";
}

int main(){

    printMensagem();
    printMensagem();
    printMensagem();

    return 0;
}
```
Compilando e rodando, teremos:

```
Número de vezes que printMensagem foi chamada: 1
Número de vezes que printMensagem foi chamada: 1
Número de vezes que printMensagem foi chamada: 1
```

O que é um pouco estranho. Não é esse o funcionamento o qual esperamos.

Agora, utilizando **static**:

```cpp
#include <iostream>

void printMensagem(){
    //Declaração com static
    static int num = 0;
    std::cout << "Número de vezes que printMensagem foi chamada: " << ++num << "\n";
}

int main(){

    printMensagem();
    printMensagem();
    printMensagem();

    return 0;
}
```
Compilando e rodando, teremos:

```
Número de vezes que printMensagem foi chamada: 1
Número de vezes que printMensagem foi chamada: 2
Número de vezes que printMensagem foi chamada: 3
```

Tendo em vista o caso representado acima,

**Exemplo 2: caso não tenha utilizado variáveis locais estáticas na implementação do primeiro exemplo, implemente mais uma vez de modo que a nova versão do seu programa utilize**

Agora, a declaração de uma variável para realizar a contagem pode ocorrer dentro do escopo de uma função. No código a seguir, a declaração aconteceu dentro do campo da função fatorial.

```cpp
#include <iostream>

int fatorial(int num){
    /* Sintaxe para definição de variável local estática.
     * Este inicializador só é executado uma vez */
    static int counter = 0;
    counter++;

    if(!num || num == 1){
        std::cout << "O número de chamadas recursivas foi: " << counter << "\n";
        return 1;
    }

    return num * fatorial(num - 1);
}


int main(){

    int numero;
    std::cout << "Insira um inteiro: ";
    std::cin >> numero;

    int fatorialNumero = fatorial(numero);
    std::cout << "O fatorial desse número é: " << fatorialNumero << "\n";
    return 0;
}

```

Compile e rode o código para ver o resultado.

Diferentemente da versão anterior, que utilizava variável global, não podemos interagir neste contexto com a variável **counter** fora do escopo da função **fatorial**. Não podemos, por exemplo, incrementá-la diretamente no corpo da **main** digitando **counter++**.

Agora a nossa variável está unicamente associada àquela função em específico. Além disso, **quando saímos do seu escopo e depois retornamos com alguma nova chamada, a variável local estática irá lembrar do seu último valor estabelecido.**

Simples assim. Essa é a principal utilidade das variáveis locais estáticas.

## Conclusões

Nesta segunda parte do Capítulo 6, você teve um primeiro contato com programação em C++ utilizando **variáveis locais estáticas**.

Não deixe de conferir o próximo capítulo! Até mais!

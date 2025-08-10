# Capítulo 6: Namespaces e variáveis locais estáticas

Sejam bem-vindos ao Capítulo 6 do nosso curso!

Quando falamos de organização de código, existem muitas ferramentas capazes de auxiliar a estruturação dele. Neste capítulo, abordaremos mais alguns pontos importantes para a criação de programas mais robustos. Começando por **namespaces**, definidos pelo programador. Em seguida, abordaremos um pouco a respeito de **Static**, no contexto de variáveis locais.

## 6.1 Namespaces:

Considere o seguinte código:

```
Main.cpp
```
```cpp
#include <iostream>

int calculaFatorial(int num){
    if(num == 1 || !num) return 1;
    return num * calculaFatorial(num - 1);
}

int entradaFatorial(){
    int num;
    std::cout << "Você quer saber o fatorial de qual número maior ou igual a zero? ";
    std::cin >> num;
    while(num < 0){
        std::cout << "Número inválido! Tente novamente" << std::endl;
        std::cin >> num;
    }
    return num;
}

void saidaFatorial(int num, long int fatorial){
    std::cout <<"O fatorial de " << num <<" é: "<< fatorial << std::endl;
}

int main(){
    int valor = entradaFatorial();
    saidaFatorial(valor, calculaFatorial(valor));
    return 0;
}
```

Aqui, temos mais um exemplo utilizando o cálculo de fatoriais. No caso, temos três funções: **calculaFatorial**, **entradaFatorial** e **saidaFatorial**.

Tudo o que "interliga" elas, na prática, é o nome o qual colocamos no cabeçalho de cada uma. Neste contexto, onde temos apenas um arquivo **.cpp**, é razoável nos basearmos em algo parecido. Porém, conforme o projeto for expandido com múltiplos arquivos e mais funções, podemos obter, no que diz respeito às definições, eventuais **colisões** ou, pelo menos, nomes cada vez mais desnecessariamente complexos.

Uma ferramenta mais elegante, chamada de **namespace**, presente na linguagem **C++** pode ser muito útil para atenuar esse problema. Observe a sintaxe:

```cpp
namespace Identificador{
    /* Área para código.
     * Podemos declarar/definir constantes/funções */
}
```

Essa utilidade nos fornece a capacidade de agrupar, em um bloco, funções, variáveis, etc, referentes a algo arbitrariamente definido pelo programador. Podemos acessar as funcionalidades presentes no namespace através, por exemplo, da sintaxe "**Identificador::**".

**Exemplo 1: faça um namespace Fatorial, com as funções as quais implementamos acima**

Primeiro, vamos realizar a definição:

```cpp
#include <iostream>

/* Ainda que você tenha a liberdade para escolher
 * o nome do seu namespace, temos como boa prática
 * utilizar letra maiúscula no primeiro caractere */

namespace Fatorial{

}

int main(){
    return 0;
}
```

Agora, com o recurso do **namespace**, não precisamos acrescentar o nome "Fatorial" na nomenclatura das nossas funções anteriores. Acompanhe:

```cpp
#include <iostream>

/* Ainda que você tenha a liberdade para escolher
 * o nome do seu namespace, temos como boa prática
 * utilizar letra maiúscula no primeiro caractere */

namespace Fatorial{

    /* Definimos as funções da mesma forma, com a
     * diferença de que não temos mais o nome "Fatorial"
     * no cabeçalho de cada função */

    int calcula(int num){
        if(num == 1 || !num) return 1;
        return num * calcula(num - 1);
    }

    int entrada(){
        int num;
        std::cout << "Você quer saber o fatorial de qual número positivo? ";
        std::cin >> num;
        while(num < 0){
            std::cout << "Número inválido! Tente novamente" << std::endl;
            std::cin >> num;
        }
        return num;
    }

    void saida(int num, long int fatorial){
        std::cout <<"O valor do fatorial de " << num <<" é: "<< fatorial << std::endl;
    }
}

/*Perceba a diferença na chamada das funções na main*/
int main(){
    int valor = Fatorial::entrada();
    Fatorial::saida(valor, Fatorial::calcula(valor));
    return 0;
}
```

É razoavelmente intuitivo o potencial existente no uso dessa ferramenta. Com ela, podemos, basicamente, "rotular" um conjunto de codificações.

E, sim! utilizamos namespaces ao digitar, por exemplo, "**std::cout**" ou "**std::cin**".

Podemos, também, organizar o código acima da seguinte forma:

```cpp
#include <iostream>

//Declaração
namespace Fatorial{
    int calcula(int num);
    int entrada();
    void saida(int num, long int fatorial);
}

int main(){
    int valor = Fatorial::entrada();
    Fatorial::saida(valor, Fatorial::calcula(valor));
    return 0;
}

//Definição
namespace Fatorial{
    int calcula(int num){
        if(num == 1 || !num) return 1;
        return num * calcula(num - 1);
    }

    int entrada(){
        int num;
        std::cout << "Você quer saber o fatorial de qual número positivo? ";
        std::cin >> num;
        while(num < 0){
            std::cout << "Número inválido! Tente novamente" << std::endl;
            std::cin >> num;
        }
        return num;
    }

    void saida(int num, long int fatorial){
        std::cout <<"O valor do fatorial de " << num <<" é: "<< fatorial << std::endl;
    }
}
```

**Exemplo 2: faça um namespace Circunferencia, com três funções nomeadas de maneira igual àquelas presentes no namespace Fatorial, sendo que calcula(double raio) retornará a circunferência calculada a partir do "raio" passado como argumento**

Vamos começar com a nossa declaração:

```cpp
namespace Circunferencia{
    /* Declaração de constantes funcionam,
     * exemplificadamente, da seguinte maneira: */
    constexpr double pi{3.14};
    double calcula(double raio);
    double entrada();
    void saida(double raio, double resultado);
}
```

Perceba que o tipo retornado e os argumentos podem ser alterados livremente com o uso dessa ferramenta.

Vejamos a implementação de cada uma das nossas funções:

```cpp
//Versão de "calcula" para Circunferencia
double calcula(double raio){
    return 2 * pi * raio;
}
```
```cpp
//Versão de "entrada" para Circunferencia
double entrada(){
    double num;
    std::cout << "Para calcular a circunferência, digite o raio: ";
    std::cin >> num;
    return num;
}
```
```cpp
//Versão de "saida" para Circunferencia
void saida(double raio, double resultado){
    std::cout << "A circunferência com raio " << raio << " é: " << resultado << std::endl;
}
```

Por fim, vamos ver como ficou o nosso programa como um todo:

```cpp
#include <iostream>

namespace Fatorial{
    int calcula(int num);
    int entrada();
    void saida(int num, long int fatorial);
}

namespace Circunferencia{
    //Declaração de constante
    constexpr double pi{3.14};
    double calcula(double raio);
    double entrada();
    void saida(double raio, double resultado);
}

int main(){
    int valor = Fatorial::entrada();
    Fatorial::saida(valor, Fatorial::calcula(valor));

    double raio = Circunferencia::entrada();
    Circunferencia::saida(raio, Circunferencia::calcula(raio));
    return 0;
}

namespace Fatorial{

    int calcula(int num){
        if(num == 1 || !num) return 1;
        return num * calcula(num - 1);
    }

    int entrada(){
        int num;
        std::cout << "Você quer saber o fatorial de qual número positivo? ";
        std::cin >> num;
        while(num < 0){
            std::cout << "Número inválido! Tente novamente" << std::endl;
            std::cin >> num;
        }
        return num;
    }

    void saida(int num, long int fatorial){
        std::cout <<"O valor do fatorial de " << num <<" é: "<< fatorial << std::endl;
    }
}

namespace Circunferencia{

    //Versão de "calcula" para Circunferencia
    double calcula(double raio){
        return 2 * pi * raio;
    }

    //Versão de "entrada" para Circunferencia
    double entrada(){
        double num;
        std::cout << "Para calcular a circunferência, digite o raio: ";
        std::cin >> num;
        return num;
    }

    //Versão de "saida" para Circunferencia
    void saida(double raio, double resultado){
        std::cout << "A circunferência com raio " << raio << " é: " << resultado << std::endl;
    }
}
```

O código acima pode ser compilado e rodado tranquilamente. Agora, você percebeu algo estranho nessa estruturação?

No exemplo acima, inicializamos uma constante na declaração do nosso novo **namespace**. Depois, apenas precisamos definir as funções declaradas.

Isso, pois, um ponto muito interessante a respeito dos **namespaces** é que temos flexibilidade na realização de declarações e definições, de modo que não precisamos, necessariamente, declarar tudo num único bloco e, depois, definir tudo num outro.

Além disso, podemos "fragmentar" nossa codificação referente àquele namespace e, mesmo assim, manter a nova programação "rotulada" simplesmente utilizando a sintaxe básica. Nitidamente, não esqueça que o compilador interpreta o nosso código sequencialmente (no que isso implica?).

**Exemplo 3: implemente mais uma função e/ou defina uma nova constante para o namespace Circunferencia, em um bloco diferente daqueles já utilizados anteriormente**

Neste exemplo, vamos implementar apenas mais uma simples função de print:

```cpp
#include <iostream>

namespace Circunferencia{
    void mensagem(){
        std::cout << "Olha essa geometria!" << std::endl;
    }
}

namespace Fatorial{
    int calcula(int num);
    int entrada();
    void saida(int num, long int fatorial);
}

namespace Circunferencia{
    //Inicialização de constante
    constexpr double pi{3.14};
    double calcula(double raio);
    double entrada();
    void saida(double raio, double resultado);
}

int main(){
    int valor = Fatorial::entrada();
    Fatorial::saida(valor, Fatorial::calcula(valor));

    double raio = Circunferencia::entrada();
    Circunferencia::saida(raio, Circunferencia::calcula(raio));

    //A chamada utiliza a mesma sintaxe. Todas as funções, exceto a main, estão rotuladas
    Circunferencia::mensagem();
    return 0;
}

/* Aqui, imagine o resto do nosso código... */
```

Faça a implementação, a compilação e rode o programa para ver o resultado.

Vamos, agora, ressaltar mais dois pontos importantes antes de visualizar o uso dos nossos **namespaces** com múltiplos arquivos e headers:

De acordo com o [Capítulo 7.2](https://www.learncpp.com/cpp-tutorial/user-defined-namespaces-and-the-scope-resolution-operator/) do site [Learn C++](https://www.learncpp.com/), temos que

"Se um identificador dentro de um namespace for usado e nenhuma resolução de escopo for fornecida, o compilador tentará primeiro encontrar uma declaração correspondente nesse mesmo namespace. Se nenhum identificador correspondente for encontrado, o compilador verificará cada namespace que o contém em sequência para ver se há uma correspondência, com o namespace global sendo verificado por último."

Considere a seguinte estruturação do código:

```cpp
#include <iostream>

void mensagem(){
    std::cout << "Olha essa ";
}

namespace Circunferencia{
    void mensagem(){
        std::cout << "geometria!" << std::endl;
    }

    void mensagemCompleta(){
        ::mensagem(); // Chamada de mensagem() do namespace global
        mensagem(); // Chamada de mensagem() do namespace Circunferencia
    }
}

int main(){
    /*Chamada de mensagem() do namespace global (equivalente à simples chamada de
     * mensagem(), neste caso) */
    ::mensagem();
    /*Chamada de mensagem() do namespace Circunferencia*/
    Circunferencia::mensagem();
    return 0;
}

```

Neste caso, se compilarmos e rodarmos, teremos a mesma mensagem sendo impressa duas vezes!

O outro detalhe importante é que podemos declarar um **namespace** dentro de outro **namespace**.

**Exemplo 4: crie um novo namespace chamado Mathematica e faça nele as declarações/definições dos outros namespaces anteriormente implementados**

Simplesmente, fazemos isso:

```cpp
#include <iostream>

namespace Mathematica{

    namespace Circunferencia{
        constexpr double pi{3.14};
        double calcula(double raio);
        double entrada();
        void saida(double raio, double resultado);
    }

    namespace Fatorial{
        int calcula(int num);
        int entrada();
        void saida(int num, long int fatorial);
    }
}

namespace Circunferencia{
    void mensagem(){
        std::cout << "Olha essa geometria!" << std::endl;
    }
}

int main(){
    /* Com a estruturação atual, podemos realizar apenas este "acesso"
     * com um único prefixo (por quê?) */
    Circunferencia::mensagem();

    /*De resto, nossa implementação pode assumir esta forma: */
    double raio = Mathematica::Circunferencia::entrada();
    Mathematica::Circunferencia::saida(raio, Mathematica::Circunferencia::calcula(raio));

    int valor = Mathematica::Fatorial::entrada();
    Mathematica::Fatorial::saida(valor, Mathematica::Fatorial::calcula(valor));
    return 0;
}

namespace Mathematica{

    namespace Fatorial{
        //Aqui, as definições
    }

    namespace Circunferencia{
        //Aqui, as definições
    }
}
```

Se quisermos que **Circunferencia::mensagem()** faça parte de **Mathematica**, sem precisarmos adicioná-lo ao corpo do novo **namespace**, podemos fazer o seguinte:

```cpp
namespace Mathematica{

    namespace Circunferencia{
        constexpr double pi{3.14};
        double calcula(double raio);
        double entrada();
        void saida(double raio, double resultado);
    }

    namespace Fatorial{
        int calcula(int num);
        int entrada();
        void saida(int num, long int fatorial);
    }
}

namespace Mathematica::Circunferencia{
    void mensagem(){
        std::cout << "Olha essa geometria!" << std::endl;
    }
}

int main(){

    Mathematica::Circunferencia::mensagem();

    double raio = Mathematica::Circunferencia::entrada();
    Mathematica::Circunferencia::saida(raio, Mathematica::Circunferencia::calcula(raio));

    int valor = Mathematica::Fatorial::entrada();
    Mathematica::Fatorial::saida(valor, Mathematica::Fatorial::calcula(valor));
    return 0;
}

namespace Mathematica{

    namespace Fatorial{
        //Aqui, as definições
    }

    namespace Circunferencia{
        //Aqui, as definições
    }
}
```

Novamente, compile e rode o código para ver o resultado.

Então, por fim, vamos falar de múltiplos arquivos e headers.

**Exemplo 5: crie um arquivo chamado **Mathematica.cpp**, mantenha as declarações no arquivo **Main.cpp** e mova as definições para o novo arquivo criado**

Vamos lá:

```
Main.cpp
```

```cpp
#include <iostream>

namespace Mathematica{

    namespace Circunferencia{
        constexpr double pi{3.14};
        double calcula(double raio);
        double entrada();
        void saida(double raio, double resultado);
    }

    namespace Fatorial{
        int calcula(int num);
        int entrada();
        void saida(int num, long int fatorial);
    }
}

namespace Mathematica::Circunferencia{
    void mensagem();
}

int main(){

    Mathematica::Circunferencia::mensagem();

    /*De resto, nossa implementação pode assumir esta forma: */
    double raio = Mathematica::Circunferencia::entrada();
    Mathematica::Circunferencia::saida(raio, Mathematica::Circunferencia::calcula(raio));

    int valor = Mathematica::Fatorial::entrada();
    Mathematica::Fatorial::saida(valor, Mathematica::Fatorial::calcula(valor));
    return 0;
}
```

```
Mathematica.cpp
```

```cpp
#include <iostream>

namespace Mathematica::Circunferencia{
    void mensagem(){
        std::cout << "Olha essa geometria!" << std::endl;
    }
}

namespace Mathematica{

    namespace Fatorial{

        int calcula(int num){
            if(num == 1 || !num) return 1;
            return num * calcula(num - 1);
        }

        int entrada(){
            int num;
            std::cout << "Você quer saber o fatorial de qual número positivo? ";
            std::cin >> num;
            while(num < 0){
                std::cout << "Número inválido! Tente novamente" << std::endl;
                std::cin >> num;
            }
            return num;
        }

        void saida(int num, long int fatorial){
            std::cout <<"O valor do fatorial de " << num <<" é: "<< fatorial << std::endl;
        }
    }

    namespace Circunferencia{

        constexpr double pi{3.14};
        double calcula(double raio){
            return 2 * Mathematica::Circunferencia::pi * raio;
        }

        double entrada(){
            double num;
            std::cout << "Para calcular a circunferência, digite o raio: ";
            std::cin >> num;
            return num;
        }

        void saida(double raio, double resultado){
            std::cout << "A circunferência com raio " << raio << " é: " << resultado << std::endl;
        }
    }
}
```

Agora, assim como aprendemos na parte 2 do Capítulo 3 do nosso curso, podemos simplesmente compilar os nossos dois arquivos conjuntamente.

Finalmente, caso queira utilizar um arquivo header:

**Exemplo 6: crie um arquivo chamado Mathematica.h, mova as declarações de Main.cpp para o novo arquivo e rode o programa**

Teremos:

```
Mathematica.h
```
```cpp
namespace Mathematica{

    namespace Circunferencia{
        constexpr double pi{3.14};
        double calcula(double raio);
        double entrada();
        void saida(double raio, double resultado);
    }

    namespace Fatorial{
        int calcula(int num);
        int entrada();
        void saida(int num, long int fatorial);
    }
}

namespace Mathematica::Circunferencia{
    void mensagem();
}
```

```
Main.cpp
```

```cpp
#include <iostream>
//Como estamos no mesmo diretório, podemos incluir desta forma:
#include "Mathematica.h"

int main(){

    Mathematica::Circunferencia::mensagem();

    /*De resto, nossa implementação pode assumir esta forma: */
    double raio = Mathematica::Circunferencia::entrada();
    Mathematica::Circunferencia::saida(raio, Mathematica::Circunferencia::calcula(raio));

    int valor = Mathematica::Fatorial::entrada();
    Mathematica::Fatorial::saida(valor, Mathematica::Fatorial::calcula(valor));
    return 0;
}
```

Perceba como o nosso arquivo **Main.cpp** ficou limpo, muito bonito e com um grau de organização muito superior.

Se exercutarmos, caso não tenha nada de incorreto, teremos o mesmo resultado da compilção/execução anterior.

## Conclusões

Nesta primeira parte do Capítulo 6, você teve um primeiro contato com programação em C++ utilizando **namespaces**.

Não deixe de conferir os próximos capítulos! Até mais!

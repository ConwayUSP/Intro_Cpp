# Capítulo 2 - Parte 1: Tipos Fundamentais de Dados

Sejam bem-vindos ao Capítulo 2 da nossa trilha!

Neste capítulo, conheceremos os tipos fundamentais de dados em C++ e um pouquinho de como nosso computador armazena e interpreta os dados que colocamos nele!

## 2.1 - Bits, Bytes e o Acesso à Memória

Na seção 1.3, comentamos brevemente em como variáveis são nomes associados a locais de memória que podem ser usados para guardar informações. Ou seja, quando uma variável é declarada em um programa, um pedaço da memória é separado para aquela variável.

A menor unidade de memória é o **dígito binário** (ou chamado de **bit**), que pode ser um valor 0 ou 1. A memória é organizada em unidades sequenciais chamadas de **endereços de mémória** (ou apenas **endereços**), que nos permitem encontrar e acessar o conteúdo da memória de um local específico.

Porém, nas arquiteturas de computador mais modernas, os bits não possuem mais um endereço único e exclusivo, pois o número de endereços de memória disponíveis são limitados e a necessidade de acessar os dados bit por bit se tornou rara. Ao invés disso, hoje em dia cada endereço de memória armazena 1 byte de dados. O **byte** é um grupo de bits que operam como uma unidade, composto por **8 bits sequenciais**.

## 2.2 - Tipos de Dados

Visto que todos os dados em um computador são uma sequência de bits, usamos os **tipos de dados** para dizer ao compilador como interpretar o conteúdo da memória em algo que tenha significado. Quando declaramos uma variável como **inteiro**, dizemos ao compilador: "Este pedaço de memória que a variável está usando deve ser interpretado como um valor inteiro". 

Tudo o que você deve fazer é escolher o tipo de dado para o seu objeto que melhor atenda o uso desejado.

## 2.3 Tipos Fundamentais de dados

O C++ já possui diversos tipos de dados predeterminados disponíveis para uso, cujos mais básicos são chamados de **tipos fundamentais de dados** (ou, informalmente, de **tipos primitivos**).

Aqui está uma lista com os tipos fundamentais de dados, que alguns você já deve ter visto.

| Tipo                                             | Categoria                | Significado                                            | Exemplo |
| -----------------------------------------------  | ------------------------ | ------------------------------------------------------ | ------- |
| `float`,`double`,`long double`                   | Ponto Flutuante          | um número decimal                                      | 3.14159 |
| `bool`                                           | Inteiro (Booleano)       | verdadeiro ou falso                                    | true    |
| `char`,`wchat_t`,`char8_t`,`char16_t`,`char32_t` | Inteiro (Caractere)      | um caractere de texto                                  | 'c'     |
| `short int`,`int`,`long int`,`long long int`     | Inteiro (Inteiro Padrão) | um número positivo ou negativo inteiro, incluindo zero | 64      |
| `std::nullptr_t `                                | Ponteiro Nulo            | um ponteiro nulo                                       | nullptr |
| `void`                                           | Void                     | sem tipo                                               | n/a     |
> Você pode estar se perguntando: por quê os tipos **char** e **bool** estão na categoria 'Inteiro' ? Ótima pergunta!
> 
> Isto é porque estes tipos são armazenados internamente como números, porém são interpretados de forma distinta do tipo **int** que é um tipo inteiro padrão, adquirindo diferentes significados para cada um deles quando realizamos a E/S.

## 2.4 - Uso do Void

Outra dúvida que pode ter surgido é: como assim **void** é um tipo "sem tipo"?

Basicamente, o tipo **void** é um **tipo incompleto**, isto é, um tipo que foi declarado mas não definido. O compilador sabe da existência do tipo de dado, porém não tem informação suficiente para determinar o quanto de memória alocar.

```cpp
void value; // não funciona, pois variáveis não podem ser definidas com tipo incompleto void
```

O tipo void é usado em diversos contextos, sendo o principal:
### Funções que não retornam valores
```cpp
void escreveValor(int x) // void aqui significa que a função não retorna nenhum valor
{
    std::cout << "The value of x is: " << x << '\n';
    // não declara return, pois a função não retorna nada
}
```
### Boas Práticas com Void
Em C, é comum usar **void** para indicar que uma função não recebe nenhum parâmetro.
```cpp
int pegarValor(void) // void aqui significa nenhum parâmetro
{
    int x{};
    std::cin >> x;

    return x;
}
```
Porém, mesmo que isto compile em C++, este uso é considerado obsoleto. O seguinte uso é equivalente e preferível por seguir as boas práticas modernas.
```cpp
int pegarValor() // parâmetros da função vazio é um void implícito
{
    int x{};
    std::cin >> x;

    return x;
}
```

## 2.5 - Tamanho de Objetos

Como vimos na parte 1 deste capítulo, a memória em computadores modernos são normalmente organizadas em unidades de tamanho equivalente a um **byte**, com cada byte contendo um endereço único. Por enquanto, foi útil pensar na memória como várias caixas de correio onde podemos colocar e retirar informações, sendo as variáveis os nomes para o acesso à essas caixas. 

No entanto, esta analogia não está totalmente correta, já que a maioria dos objetos ocupam mais do que 1 byte de memória. Um único objeto pode ocupar de 1, 2, 4, 8, ou até mais endereços de memória consecutivos, dependendo do tipo de dado armazenado.

Como acessamos a memória através dos nomes das variáveis que criamos, o compilador esconde os detalhes de quantos bytes de memória um objeto usa de fato. Isto é útil para que em alto nível de programação não tenhamos que saber quantos bytes de dados devem ser acessados para manipular as variáveis que criamos. Mesmo assim, há muitas razões onde saber o quanto de memória um objeto usa se torna útil, isto porquê:

### Quanto mais memória um objeto usa, mais informações ele consegue conter:

Vejamos:                                               
1 bit consegue armazenar 2 valores possíveis, sendo eles: 0 ou 1.                        
2 bits conseguem armazenar 4 valores possíveis, sendo eles: 00, 01, 10 ou 11.                  
3 bits conseguem armazenar 8 valores possíveis, sendo eles: 000, 001, 010, 011, 100, 101, 110 ou 111.

Se generalizarmos, um objeto com **n** bits consegue armazenar **2<sup>n</sup>** valores únicos. Isto é, um objeto com o tamanho de 1 byte consegue armazenar 2<sup>8</sup> (256) valores diferentes. Um objeto com o tamanho de 2 bytes consegue armazenar 2<sup>16</sup> (65536) valores diferentes. E assim em diante!

Então, o tamanho de um objeto coloca um limite na quantidade de valores únicos que ele consegue armazenar, e quanto mais bytes de memória, maior o número de valores únicos armazenados. Computadores tem um número finito de memória disponível, e sempre que definimos um objeto, uma pequena parte desta memória livre é usada enquanto o objeto existir. Como os computadores de hoje em dia possuem muita memória, geralmente o impacto disso é quase sempre imperceptível. Mas para programas que precisam de objetos e dados em grande quantidade, a diferença entre usar 1 byte e 8 bytes pode ser significativa!

Sabendo disso, nos perguntamos: "Então quanto de memória os objetos de cada tipo de dado usam?". 
Surpreendentemente, o C++ não define o tamanho exato em bits de nenhum dos tipos fundamentais.

Ao invés disso, o padrão diz o seguinte:
- Um objeto deve ocupar pelo menos 1 byte (para que cada objeto tenha um endereço de memória distinto);
- Um byte deve ter pelo menos 8 bits;
- Os tipos inteiros `char`,`short`,`ìnt`,`long`, e `long long` tem um tamanho mínimo de 8, 16, 16, 32 e 64 bits respectivamente;
- `char` e `char8_t` tem exatamente 1 byte.

>**Observação:** Quando falamos "tamanho de um tipo", queremos dizer o tamanho de um objeto instanciado daquele tipo.
>
>Se quiser saber mais sobre o padrão do C++ sobre o tamanho mínimo dos vários tipos de dados, considere dar uma lida [aqui](https://en.cppreference.com/w/cpp/language/types.html).

## 2.6 - O operador sizeof

Para determinar o tamanho dos tipos de dados em cada máquina específica, o C++ fornece um operador chamado `sizeof`. O **operador sizeof** é um operador **unário** (que só recebe uma entrada) que recebe um tipo ou variável, e retorna o tamaho de um objeto daquele tipo (em bytes).
Por exemplo:

```cpp
#include <iostream>
#include <climits> // para o CHAR_BIT

int main()
{
    std::cout << "Um byte é " << CHAR_BIT << " bits\n\n";

    std::cout << "bool: " << sizeof(bool) << " bytes\n";
    std::cout << "char: " << sizeof(char) << " bytes\n";
    std::cout << "short: " << sizeof(short) << " bytes\n";
    std::cout << "int: " << sizeof(int) << " bytes\n";
    std::cout << "long: " << sizeof(long) << " bytes\n";
    std::cout << "long long: " << sizeof(long long) << " bytes\n";
    std::cout << "float: " << sizeof(float) << " bytes\n";
    std::cout << "double: " << sizeof(double) << " bytes\n";
    std::cout << "long double: " << sizeof(long double) << " bytes\n";

    return 0;
}
```
Compilando e executando este código na máquina do autor deste capítulo, temos a seguinte saída:
```
Um byte é 8 bits

bool: 1 bytes
char: 1 bytes
short: 2 bytes
int: 4 bytes
long: 8 bytes
long long: 8 bytes
float: 4 bytes
double: 8 bytes
long double: 16 bytes
```
O resultado vai depender do compilador, arquitetura de computador, sistema operacional, configurações da compilação (32-bits ou 64-bits), e etc.

Também é possível usar o operador `sizeof` em um nome de variável, como em:
```cpp
#include <iostream>

int main()
{
    int x{};
    std::cout << "x é " << sizeof(x) << " bytes\n";

    return 0;
}
```
Recebemos a seguinte saída:
```
x é 4 bytes
```
>O operador `sizeof` não inclui memória alocada dinamicamente usada por um objeto. Memórica alocada dinamicamente será discutido em futururos capítulos! Fiquem de olho!

## Conclusões

Agora você conhece um pouco mais dos tipos fundamentais de dados em C++ e em como é armazenada a memória do nosso queridinho computador!

Mas atenção! Aqui passamos apenas pelo básico, então ainda precisamos estudar um pouco dos chamados "tipos compostos de dados", como strings, matrizes, structs entre outros, tipos estes que já se tornaram padrão na biblioteca de C++ e que muitas vezes precisam ser declarados para uso! Felizmente, abordaremos muitos destes temas em futuros capítulos, espero você por lá!

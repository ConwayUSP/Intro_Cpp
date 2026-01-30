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
## Conclusões

Agora você conhece um pouco mais dos tipos fundamentais de dados em C++ e em como é armazenada a memória do nosso queridinho computador!

Mas atenção! Aqui passamos apenas pelo básico, então ainda precisamos estudar um pouco dos chamados "tipos compostos de dados", como strings, matrizes, structs entre outros, tipos estes que já se tornaram padrão na biblioteca de C++ e que muitas vezes precisam ser declarados para uso! Felizmente, abordaremos muitos destes temas em futuros capítulos, espero você por lá!


# Capítulo 04 - Parte 1: Variáveis e expressões constantes

Bem vindos ao Capítulo 4!

Neste capítulo nós focaremos no tipo de constantes nomeadas, que são valores constantes associados a um identificador e vamos apresentar as variáveis e expressões constantes, além do uso de variáveis constexpr.

## 4.1 Variáveis constantes

A utilização de **variáveis constantes** surge a partir da necessidade de definir valores que não podem ser alterados durante a execução do programa como, por exemplo, o valor da velocidade da luz: 299.792.458×10⁸ metros/segundo.

Esse valor é bem improvável que mude (e se mudar, bem, acho você terá problemas maiores do que estar preocupado em mudar esse valor no seu código).

Declarando uma variável constante:

```cpp
const double LIGHT_SPEED_CONST = 2.99792458e8; // em metros por segundo
const double GRAVITY { 9.8 }; // em metros/segundo²
```

Lembre-se que variáveis constantes devem ser inicializadas quando você as define, e caso você não declare seu valor, a constante pode ter qualquer valor que esteja na memória do computador naquele momento da declaração da variável.

Além disso, variáveis constantes podem ser inicializadas a partir de outras variáveis (incluindo aquelas não constantes):

```cpp
#include <iostream>

int main()
{
    std::cout << "Digite sua idade: ";
    int idade{};
    std::cin >> idade;

    const int constIdade { idade }; // incializando variável constante usando um valor não constante

    idade = 5;      // ok: idade não é const, então pode-se mudar seu valor
    constIdade = 6; // erro: constIdade é const, então não podemos mudar seu valor

    return 0;
}
```

## 4.2 Expressões constantes

Em C++, uma "expressão constante" é uma expressão que deve ser avaliável em tempo de compilação. 

Para declararmos uma expressão constante utilizamos **constexpr**, que deve ser inicializada com uma expressão constante, caso contrário, ocorrerá um erro de compilação.

Veja o exemplo a seguir: 

```cpp
#include <iostream>

// O valor retornado por uma função não‑constexpr não é constexpr
int cinco()
{
    return 5;
}

int main()
{
    constexpr double gravidade { 9.8 };        // ok: 9.8 é uma expressão constante
    constexpr int soma       { 4 + 5 };        // ok: 4 + 5 é uma expressão constante
    constexpr int algo       { soma };         // ok: soma é uma expressão constante

    std::cout << "Digite sua idade: ";
    int idade{};
    std::cin >> idade;

    constexpr int minhaIdade       { idade };  // erro de compilação: idade não é expressão constante
    constexpr int resultadoCinco   { cinco() }; // erro de compilação: retorno de cinco() não é constexpr

    return 0;
}
```

Como as funções normalmente são executadas em tempo de execução, o valor de retorno de uma função não é constexpr (mesmo quando a expressão de retorno é uma expressão constante). 

É por isso que 'cinco()' não é um valor de inicialização válido para constexpr int resultadoCinco.

## Questões

1) Crie um programa que:
- Declare duas variáveis const representando:

    O valor de π (3.14159)

    A velocidade do som (343.2 m/s)
- Peça ao usuário o raio de uma circunferência e calcule o perímetro usando a constante π.
- Exiba o resultado.

2) Crie um programa que peça ao usuário:
   
    O valor de um produto
   
    A porcentagem de desconto

- Use uma constante const para armazenar a taxa de imposto (por exemplo, 5%).
- Calcule o valor com desconto e o valor final com imposto
- Explique por que não é possível armazenar o valor com desconto em uma variável constexpr.
## Conclusões

Nessa primeira parte do capítulo 4 foram apresentados os usos de variáveis e expressões constantes em C++.

Resumindo a diferença entre **const** e **constexpr**:

* **const**: significa que o valor de um objeto não pode ser alterado após a inicialização. O valor do inicializador pode ser conhecido em tempo de compilação ou de execução. O objeto const pode ser avaliado em tempo de execução.
  
* **constexpr**: significa que o objeto pode ser usado em uma expressão constante. O valor do inicializador deve ser conhecido em tempo de compilação. O objeto constexpr pode ser avaliado em tempo de execução ou de compilação.

Aguardo você na próxima parte!

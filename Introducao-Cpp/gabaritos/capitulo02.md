# Capítulo 02

## Parte 1: Tipos Fundamentais de Dados

### Exercício 1: Tamanho dos tipos long long e long double

```cpp
#include <iostream>

int main()
{
    // Obtendo o tamanho em bytes de long long e long double
    int tamanhoLongLong = sizeof(long long);
    int tamanhoLongDouble = sizeof(long double);

    // Calculando a soma
    int soma = tamanhoLongLong + tamanhoLongDouble;

    // Exibindo os resultados
    std::cout << "Tamanho de long long: " << tamanhoLongLong << " bytes\n";
    std::cout << "Tamanho de long double: " << tamanhoLongDouble << " bytes\n";
    std::cout << "Soma dos tamanhos: " << soma << " bytes\n";

    return 0;
}
```

---

### Exercício 2: Valores possíveis em um char

```cpp
#include <iostream>
#include <cmath> // para a função pow()

int main()
{

    int tamanhoChar = sizeof(char);
    int bitsChar = tamanhoChar * 8;  // Considerando que 1 byte = 8 bits

    // Valores Possíveis = 2 elevado à quantidade de bits
    int valoresPossiveis = pow(2, bitsChar); // Calcula 2^bitsChar

    std::cout << "Uma variável do tipo char armazena " << tamanhoChar << " byte(s) (" << bitsChar << " bits) e ";
    std::cout << "pode armazenar " << valoresPossiveis << " valores diferentes.\n";

    return 0;
}
```

---

## Parte 2: Trabalhando com os Tipos de Dados

### Exercício 1: Conversão de double para int

```cpp
#include <iostream>

int main()
{
    double numeroDecimal;

    std::cout << "Digite um número decimal: ";
    std::cin >> numeroDecimal;

    // Conversão explícita usando static_cast
    int numeroInteiro = static_cast<int>(numeroDecimal);

    std::cout << "O valor " << numeroDecimal << " convertido para int é: " << numeroInteiro << '\n';

    return 0;
}
```

---

### Exercício 2: Verificando se um número é positivo, negativo ou zero

```cpp
#include <iostream>

int main()
{
    int numero;

    std::cout << "Digite um número inteiro: ";
    std::cin >> numero;

    if (numero > 0)
        std::cout << "O número é positivo.\n";
    else if (numero < 0)
        std::cout << "O número é negativo.\n";
    else
        std::cout << "O número é zero.\n";

    return 0;
}
```

---

### Exercício 3: Caractere para valor ASCII

```cpp
#include <iostream>

int main()
{
    char caractere;

    std::cout << "Digite um caractere: ";
    std::cin >> caractere;

    // Convertendo explicitamente o char para int para ver seu valor ASCII
    int valorAscii = static_cast<int>(caractere);

    std::cout << "O caractere '" << caractere << "' tem o valor ASCII: " << valorAscii << '\n';

    return 0;
}
```

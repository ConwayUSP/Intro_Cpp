# Capítulo 05

## Parte 1: Controle de Fluxo

### Exercício 1: Dias da semana com switch

```cpp
#include <iostream>

int main()
{
    int dia;
    std::cout << "Digite um número de 1 a 7: ";
    std::cin >> dia;

    switch (dia)
    {
        case 1:
            std::cout << "Domingo\n";
            break;
        case 2:
            std::cout << "Segunda-feira\n";
            break;
        case 3:
            std::cout << "Terça-feira\n";
            break;
        case 4:
            std::cout << "Quarta-feira\n";
            break;
        case 5:
            std::cout << "Quinta-feira\n";
            break;
        case 6:
            std::cout << "Sexta-feira\n";
            break;
        case 7:
            std::cout << "Sábado\n";
            break;
        default:
            std::cout << "Dia inválido!\n";
            break;
    }

    return 0;
}
```

---

### Exercício 2: Identificando vogais com fallthrough

```cpp
#include <iostream>

int main()
{
    char letra;
    std::cout << "Digite uma letra: ";
    std::cin >> letra;

    switch (letra)
    {
        case 'a':
        case 'e':
        case 'i':
        case 'o':
        case 'u':
        case 'A':
        case 'E':
        case 'I':
        case 'O':
        case 'U':
            std::cout << "É uma vogal!\n";
            break;
        default:
            std::cout << "É uma consoante ou outro caractere!\n";
            break;
    }

    return 0;
}
```

---

## Parte 2: Continuação de Controle de Fluxo

### Exercício 1: Somando números positivos com while

```cpp
#include <iostream>

int main()
{
    int num;
    int soma = 0;

    std::cout << "Digite um número (negativo para sair): ";
    std::cin >> num;

    while (num >= 0)
    {
        soma += num;
        std::cout << "Digite um número (negativo para sair): ";
        std::cin >> num;
    }

    std::cout << "Soma dos números positivos: " << soma << '\n';

    return 0;
}
```

---

### Exercício 2: Menu interativo com do-while

```cpp
#include <iostream>

int main()
{
    int opcao;

    do
    {
        std::cout << "\nMenu:\n";
        std::cout << "1. Opção 1\n";
        std::cout << "2. Opção 2\n";
        std::cout << "3. Opção 3\n";
        std::cout << "4. Sair\n";
        std::cout << "Escolha uma opção: ";
        std::cin >> opcao;

        switch (opcao)
        {
            case 1:
                std::cout << "Opção 1 selecionada.\n";
                break;
            case 2:
                std::cout << "Opção 2 selecionada.\n";
                break;
            case 3:
                std::cout << "Opção 3 selecionada.\n";
                break;
            case 4:
                std::cout << "Encerrando...\n";
                break;
            default:
                std::cout << "Opção inválida!\n";
                break;
        }
    } while (opcao != 4);

    return 0;
}
```

---

### Exercício 3: Pulando múltiplos de 3 com for e continue

```cpp
#include <iostream>

int main()
{
    for (int i = 1; i <= 20; ++i)
    {
        if (i % 3 == 0)
            continue; // pula os múltiplos de 3

        std::cout << i << ' ';
    }

    std::cout << '\n';

    return 0;
}
```

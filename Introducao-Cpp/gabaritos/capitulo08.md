# Capítulo 08

## Referências e Ponteiros

### Exercício 1: identificação de endereços

```cpp
#include <iostream>

int main() {
    // 1. Declare uma variável inteira chamada numero com o valor 100
    int numero = 100;

    // 2. Imprima o endereço de memória de numero
    std::cout << "Endereco de numero (&numero): " << &numero << std::endl;

    // 3. Declare um ponteiro ptr e inicialize com o endereço de numero
    int* ptr = &numero;

    // 4. Imprima o valor armazenado dentro de ptr (o endereço)
    std::cout << "Valor dentro do ponteiro (ptr): " << ptr << std::endl;

    return 0;
}
```

### Exercício 2:

```cpp
#include <iostream>

int main() {
    // 1. Variável original
    int pontuacao = 0;

    // 2. Ponteiro apontando para a variável
    int* ptrScore = &pontuacao;

    // 3. Alterando para 50 via ponteiro (desreferência)
    *ptrScore = 50;
    std::cout << "Valor apos primeira alteracao: " << pontuacao << std::endl;

    // 4. Multiplicando o valor atual por 2 via ponteiro
    *ptrScore = *ptrScore * 2;
    std::cout << "Valor final (multiplicado): " << pontuacao << std::endl;

    return 0;
}
```

### Exercício 3: Segurança com nullptr

```cpp
#include <iostream>

int main() {
    // 1. Inicializa com nullptr (boa prática)
    int* ptrSeguro = nullptr;

    int valor = 42;

    // 2. Verificação de segurança
    if (ptrSeguro == nullptr) {
        std::cout << "O ponteiro esta vazio" << std::endl;
    }

    // 3. Atribui o endereço e acessa o valor
    ptrSeguro = &valor;
    
    // Imprime via desreferência
    std::cout << "Valor apontado agora: " << *ptrSeguro << std::endl;

    return 0;
}
```

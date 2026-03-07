# Capítulo 11

### Exercício 1: Alocação Simples de Real

```cpp
#include <iostream>

int main() {
    // Alocando memória dinamicamente para um double
    // O 'new' reserva espaço na Heap e retorna o endereço
    double* ptrNumero = new double;

    std::cout << "Digite um número real (lembre-se de usar "."): ";
    std::cin >> *ptrNumero; // Guardando o valor no endereço apontado

    // Exibindo o dobro
    std::cout << "O dobro de " << *ptrNumero << " é " << (*ptrNumero * 2) << std::endl;

    // Desalocação correta
    delete ptrNumero; 

    // Anulando o ponteiro (evita o "ponteiro solto" ou dangling pointer)
    ptrNumero = nullptr;

    return 0;
}
```

### Exercício 2: Array Dinâmico de Notas

```cpp
#include <iostream>

int main() {
    int quantidade;

    std::cout << "Quantas notas deseja registrar? ";
    std::cin >> quantidade;

    // Alocando um array dinâmico com o tamanho escolhido
    double* notas = new double[quantidade];
    double soma = 0.0;

    // Preenchendo o array
    for (int i = 0; i < quantidade; i++) {
        std::cout << "Digite a nota " << i + 1 << ": ";
        std::cin >> notas[i];
        soma += notas[i];
    }

    // Cálculo da média aritmética:
    double media = soma / quantidade;

    std::cout << "\nA média das " << quantidade << " notas é: " << media << std::endl;

    // Liberando a memória de um array (importante usar o [])
    delete[] notas;
    notas = nullptr;

    return 0;
}
```

### Exercício 3: Caça ao erro

No trecho analisado, existem **dois erros críticos** que causariam problemas graves em sistemas reais:

1. **Vazamento de Memória (Memory Leak):**

- O problema: Dentro do bloco `if (ptr[0] > 0)`, o comando `return;` encerra a função imediatamente. Como o `delete` está no final da função, ele nunca é executado se a condição for verdadeira. A memória alocada para os 10 inteiros fica "presa" e inacessível até o programa fechar.

- A correção: Deve-se chamar o `delete[] ptr;` antes do `return`.

2. **Uso incorreto do operador `delete`:**

- O problema: O código usa `delete ptr;`, mas a memória foi alocada com `new int[10]`.

- A correção: Sempre que você usar `new[]` (para arrays), deve obrigatoriamente usar `delete[]`. Usar o `delete` simples em um array resulta em comportamento indefinido, podendo corromper a memória ou travar o programa.


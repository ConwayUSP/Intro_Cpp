# Capítulo 10

## Parte 1

### Exercício 1: Refatoração para for-each

```cpp
std::vector<int> numeros = {4, 5, 6};

// Versão moderna e segura
for (int n : numeros) {
    std::cout << n << " ";
}
```

### Exercício 2: Análise de Fluxo do Vector

**A saída do código será: 10 99 2 3 5**

Passo a passo da memória:

- Inicialização: `v = {1, 2, 3}`

- `insert(v.begin() + 1, 99)`: O 99 é "empurrado" para a posição 1. O vetor vira `{1, 99, 2, 3}`.

- `push_back(5)`: O 5 é adicionado ao final. O vetor vira `{1, 99, 2, 3, 5}`.

- `v.at(0) = 10:` O primeiro elemento (índice 0), que era 1, é alterado para 10.

- Resultado final: `{10, 99, 2, 3, 5}`.

### Exercício 3: Programa de Lista de Compras

```cpp
#include <iostream>
#include <vector>
#include <string>

int main() {
    std::vector<std::string> listaCompras;
    std::string item;

    std::cout << "--- Lista de Compras (digite 'fim' para encerrar) ---" << std::endl;

    while (true) {
        std::cout << "Item: ";
        std::cin >> item;

        if (item == "fim") {
            break; // Sai do laço se o usuário digitar "fim"
        }

        listaCompras.push_back(item);
    }

    std::cout << "\nSua lista final:" << std::endl;

    // Usando for-each para exibir os itens
    // O 'const &' evita cópias desnecessárias de strings longas
    for (const std::string& i : listaCompras) {
        std::cout << "- " << i << std::endl;
    }

    // Exibindo o total usando .size()
    std::cout << "\nTotal de itens: " << listaCompras.size() << std::endl;

    return 0;
}
```

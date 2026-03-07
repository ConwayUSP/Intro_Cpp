# Capítulo 07

## Parte 1

### Exercício 1: Constantes e Circunferência

```cpp
#include <iostream>
#include <string>

// 1. Template de função para tipos numéricos
// O 'T' serve como um "espaço reservado" para qualquer tipo que suporte o operador +
template <typename T>
T somar(T a, T b) {
    return a + b;
}

// 2. Sobrecarga específica para std::string
// Note que não usamos 'template' aqui; é uma função comum que "vence" o template quando os argumentos são strings.

std::string somar(std::string a, std::string b) {
    return a + " e " + b;
}

int main() {
    // Teste com inteiros (usa o template)
    // 2 + 3 = 5
    std::cout << "Soma de inteiros: " << somar(2, 3) << std::endl;

    // Teste com double (usa o template)
    // 2.5 + 3.1 = 5.6
    std::cout << "Soma de decimais: " << somar(2.5, 3.1) << std::endl;

    // Teste com strings
    // Aqui o C++ identifica que existe uma função específica e a prioriza
    std::string nome1 = "Ana";
    std::string nome2 = "João";
    
    // Importante: passamos variáveis do tipo std::string para garantir que a sobrecarga seja chamada corretamente.
    std::cout << "Soma de strings: " << somar(nome1, nome2) << std::endl;

    return 0;
}
```

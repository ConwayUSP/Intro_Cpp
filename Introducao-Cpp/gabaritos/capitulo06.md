# Capítulo 06

## Parte 1: Namespaces

### Exercício 1: Organização de Conversores

```cpp
#include <iostream>

namespace ConversorPeso {
    double converte(double kg) {
        return kg * 2.204;
    }
}

namespace ConversorTemperatura {
    double converte(double celsius) {
        return celsius * 1.8 + 32;
    }
}

int main() {
    double pesoKg = 70.0;
    double tempC = 25.0;

    std::cout << pesoKg << "kg em libras: " << ConversorPeso::converte(pesoKg) << std::endl;
    std::cout << tempC << "C em Fahrenheit: " << ConversorTemperatura::converte(tempC) << std::endl;

    return 0;
}
```

### Exercício 2: Geometria Espacial (Aninhados)

```cpp
#include <iostream>

namespace Geometria {
    namespace Area {
        double quadrado(double lado) { return lado * lado; }
    }
    namespace Volume {
        double cubo(double lado) { return lado * lado * lado; }
    }
}

int main() {
    double L = 5.0;
    std::cout << "Area: " << Geometria::Area::quadrado(L) << std::endl;
    std::cout << "Volume: " << Geometria::Volume::cubo(L) << std::endl;
    return 0;
}
```

### Exercício 3: Gestão de Inventário (Apelidos e Resolução Global)

```cpp
#include <iostream>

// 1. Função no namespace global
void exibirVersao() {
    std::cout << "Versao Global 1.0" << std::endl;
}

// 2. Namespace aninhado longo
namespace Sistema {
    namespace Logistica {
        namespace Inventario {
            void exibirVersao() {
                std::cout << "Versao do Sistema de Inventario 2.4" << std::endl;
            }
        }
    }
}

int main() {
    // 3. Criando um apelido (alias) para o namespace longo
    namespace Inv = Sistema::Logistica::Inventario;

    // 4. Chamada via apelido
    Inv::exibirVersao();

    // 5. Chamada da função global usando o operador de resolução de escopo
    ::exibirVersao();

    return 0;
}
```


## Parte 2: Variáveis Locais Estáticas

### Exercício 1: Identificador Único

```cpp
#include <iostream>

int gerarID() {
    // A variável estática preserva o valor entre as chamadas
    static int id = 0; 
    return ++id;
}

int main() {
    for(int i = 0; i < 3; ++i) {
        std::cout << "Processando tarefa ID: " << gerarID() << std::endl;
    }
    return 0;
}
```

### Exercício 2: Somatório Acumulado

```cpp
#include <iostream>

void adicionarAoTotal(int valor) {
    // A variável estática é inicializada apenas uma vez
    static int somaTotal = 0; 
    
    somaTotal += valor;
    std::cout << "Valor adicionado: " << valor << " | Subtotal atual: " << somaTotal << std::endl;
}

int main() {
    int numero;
    
    for(int i = 0; i < 5; ++i) {
        std::cout << "Digite um numero para somar: ";
        std::cin >> numero;
        adicionarAoTotal(numero);
    }
    
    return 0;
}
```

### Exercício 3: Limitador de Acesso

```cpp
#include <iostream>

void tentarAcesso() {
    // Contador estático para rastrear o histórico de execuções
    static int tentativas = 0;
    tentativas++;

    if (tentativas <= 3) {
        std::cout << "Tentativa " << tentativas << ": Acesso permitido" << std::endl;
    } else {
        std::cout << "Tentativa " << tentativas << ": Acesso bloqueado - Limite atingido" << std::endl;
    }
}

int main() {
    // Testando o limite de 3 acessos
    for(int i = 0; i < 5; ++i) {
        tentarAcesso();
    }

    return 0;
}
```

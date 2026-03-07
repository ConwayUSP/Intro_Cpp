# Capítulo 04

## Parte 1

### Exercício 1: Constantes e Circunferência

```cpp
#include <iostream>

int main() {
    // Declaração de constantes
    // 'const' impede que os valores sejam alterados durante a execução
    const double PI = 3.14159;
    const double VELOCIDADE_SOM = 343.2; // Unidade: m/s

    double raio;

    std::cout << "Digite o raio da circunferência: ";
    std::cin >> raio;

    // Cálculo do perímetro: 2 * PI * raio
    double perimetro = 2 * PI * raio;

    std::cout << "O perímetro da circunferência é: " << perimetro << std::endl;
    // Opcional
    std::cout << "Apenas como curiosidade, a velocidade do som é " << VELOCIDADE_SOM << " m/s." << std::endl;

    return 0;
}
```

### Exercício 2: Cálculo de Desconto e Imposto

```cpp
#include <iostream>

int main() {
    const double TAXA_IMPOSTO = 0.05; // 5% de imposto
    double precoProduto, porcentagemDesconto;

    std::cout << "Digite o valor do produto: ";
    std::cin >> precoProduto;

    std::cout << "Digite a porcentagem de desconto (ex: 10 para 10%): ";
    std::cin >> porcentagemDesconto;

    // Cálculo do valor com desconto
    double valorDesconto = precoProduto * (porcentagemDesconto / 100.0);
    double precoComDesconto = precoProduto - valorDesconto;

    // Cálculo do valor final com imposto
    double precoFinal = precoComDesconto * (1 + TAXA_IMPOSTO);

    std::cout << "\n--- Resumo Financeiro ---" << std::endl;
    std::cout << "Preço com desconto: R$ " << precoComDesconto << std::endl;
    std::cout << "Preço final (com 5% de imposto): R$ " << precoFinal << std::endl;

    return 0;
}
```

- O qualificador `constexpr` exige que o valor da variável seja conhecido em tempo de compilação. Como o valor do desconto depende de dados que o usuário digita enquanto o programa já está rodando (tempo de execução), o compilador não tem como prever esse resultado antecipadamente.

## Parte 2

### Exercício 1: Leitura de Nome Completo

```cpp
#include <iostream>
#include <string>

int main() {
    std::string nomeCompleto;

    std::cout << "Digite seu nome completo: ";
    // Usamos getline para capturar espaços em branco
    std::getline(std::cin >> std::ws, nomeCompleto); 

    std::cout << "Olá, " << nomeCompleto << "!" << std::endl;
    std::cout << "Seu nome possui " << nomeCompleto.length() << " caracteres (incluindo espaços)." << std::endl;

    return 0;
}
```

### Exercício 2: Conversão de Idade

```cpp
#include <iostream>
#include <string>

int main() {
    int idade;

    std::cout << "Digite sua idade: ";
    std::cin >> idade;

    // Conversão de inteiro para string
    std::string idadeStr = std::to_string(idade);

    // Concatenação de strings
    std::string frase = "Você tem " + idadeStr + " anos.";

    std::cout << frase << std::endl;

    return 0;
}
```

- Inteiro (20): É um valor numérico armazenado de forma binária na memória. Ele permite operações matemáticas (soma, subtração, etc.).

- String ("20"): É uma sequência de caracteres de texto ('2' e '0'). O computador a interpreta como um símbolo gráfico, não como uma quantidade. Você não pode somar "20" + 5 diretamente para obter 25; o resultado seria um erro ou uma concatenação textual.

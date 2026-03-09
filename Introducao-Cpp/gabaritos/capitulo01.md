# Capítulo 01

## Parte 1

### Exercício 1: Identificação de Componentes

Para a linha `std::string cidade = "São Paulo";` , os componentes são:

- **Tipo do objeto**: std::string (uma classe da biblioteca padrão para manipular sequências de caracteres).

- **Valor armazenado**: "São Paulo" (um literal de string).

- **Nome (identificador)**: cidade.

### Exercício 2: Programa de Cálculo de Idade 

```cpp
// Exemplo de resposta

#include <iostream>

int main() {
    // 1. Declaração das variáveis para armazenar os anos
    // Usamos 'int' porque anos são números inteiros.
    int anoNascimento = 2005; 
    int anoAtual = 2026;

    // 2. Cálculo da idade
    // Subtraímos o ano de nascimento do ano atual
    int idade = anoAtual - anoNascimento;

    // 3. Exibição do resultado
    // O std::cout envia o texto e o valor da variável para o terminal
    std::cout << "Com base nos dados informados, voce tem (ou fará) " 
              << idade << " anos em " << anoAtual << "." << std::endl;

    return 0;
}
```

## Parte 2

### Exercício 1: Exemplo de Soma Simples

```cpp
#include <iostream>

int main() {
    // Calculando e imprimindo diretamente
    std::cout << "A soma de 3 e 5 é " << 3 + 5 << '\n';
    
    return 0;
}
```

### Exercício 2: Programa de Saudação

```cpp
#include <iostream>
#include <string>

int main() {
    std::string nome;
    int idade;

    std::cout << "Digite o seu nome: ";
    std::cin >> nome;

    std::cout << "Digite a sua idade: ";
    std::cin >> idade;

    // Exibindo a mensagem com as variaveis
    std::cout << "Olá " << nome << ", você tem " << idade << " anos!" << std::endl;

    return 0;
}
```

### Exercício 3: "Máquina do Tempo" em C++

```cpp
#include <iostream>
#include <string>

int main() {
    std::string nome;
    int idade, anosFuturos;

    // Entrada de dados
    std::cout << "Qual o seu nome? ";
    std::cin >> nome;

    std::cout << "Quantos anos voce tem? ";
    std::cin >> idade;

    std::cout << "Quantos anos voce quer avancar no tempo? ";
    std::cin >> anosFuturos;

    // Processamento: calculando a idade futura
    int novaIdade = idade + anosFuturos;

    // Saida de dados formatada
    std::cout << "Olá " << nome << ", daqui a " << anosFuturos 
              << " anos voce terá " << novaIdade << " anos!" << std::endl;

    return 0;
}
```

## Parte 3

### Exercício 1: Expressão Booleana

```cpp
(idade > 18 && idade <= 30)
```

### Exercício 2: Análise da Expressão Complexa

- O **valor de x** será **100**.

Ordem de avaliação (Precedência):

- Parênteses: (2 + 3) vira 5.

- Aritmética: 5 * 4 vira 20 e 8 % 3 (resto da divisão) vira 2.

- Relacionais: 20 > 10 é true (verdadeiro) e 2 == 2 é true.

- Lógico: true && true resulta em true.

- Ternário: Como a condição foi verdadeira, ele escolhe o primeiro valor após a interrogação: 100.

### Exercício 3: Programa de Aprovação

```cpp
#include <iostream>

int main() {
    double nota;
    int frequencia;

    // Entrada de dados
    std::cout << "Digite a nota final (0.0 - 10.0): ";
    std::cin >> nota;

    std::cout << "Digite a frequencia (0 - 100): ";
    std::cin >> frequencia;

    // Verificação de aprovação usando operadores lógicos
    // A condição exige que AMBAS sejam verdadeiras
    bool aprovado = (nota >= 6.0 && frequencia >= 75);

    // Uso do operador ternário para decidir a mensagem
    std::string resultado = aprovado ? "Aprovado" : "Reprovado";

    // Saída
    std::cout << "Situacao do aluno: " << resultado << std::endl;

    return 0;
}
```

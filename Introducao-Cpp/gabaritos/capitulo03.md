# Capítulo 03

## Parte 1: Introdução às funções

### Exercício 1: Soma Recursiva

```cpp
#include <iostream>

// Declaração prévia
int calculaSoma(int num);

int main() {
    int n = 4;
    std::cout << "A soma de 1 ate " << n << " e: " << calculaSoma(n) << std::endl;
    return 0;
}

// Implementação do corpo
int calculaSoma(int num) {
    // Caso base: se o número chegar a 1, a soma encerra
    if (num <= 1) return 1; 
    
    // Chamada recursiva: soma o número atual com o resultado do anterior
    return num + calculaSoma(num - 1); 
}
```

### Exercício 2: Comparação de Valores

```cpp
#include <iostream>

// Declaração prévia
int menorValor(int num1, int num2);

int main() {
    int a = 7, b = 3;
    std::cout << "O menor valor entre " << a << " e " << b << " e: " 
              << menorValor(a, b) << std::endl;
    return 0;
}

// Implementação utilizando operador ternário
int menorValor(int num1, int num2) {
    // num1 é menor que num2? Se sim, retorne num1. Caso contrário, num2.
    return (num1 < num2) ? num1 : num2; 
}
```

### Exercício 3: Procedimento de Exibição

```cpp
#include <iostream>

// Declaração prévia
void exibeResultado(int valor);

int main() {
    int resultadoFinal = 42;
    
    // Chamada de função void (não pode ser atribuída a uma variável)
    exibeResultado(resultadoFinal); 
    
    return 0;
}

// Implementação da função void
void exibeResultado(int valor) {
    std::cout << "O resultado processado foi: " << valor << std::endl;
    // Note que não há comando 'return' com valor aqui
}
```

## Parte 2: Introdução a Programas com Múltiplos Arquivos

### Exercício 1: Duelo de LPs

Arquivo `main.cpp`:

```cpp
#include <iostream>

// Declaração da função que reside em outro arquivo
int atualizaLP(int lpAtual, int dano);

int main() {
    int lp = 8000;
    int danoRecebido = 1500;
    
    lp = atualizaLP(lp, danoRecebido);
    
    std::cout << "Pontos de Vida restantes: " << lp << std::endl;
    return 0;
}
```

Arquivo `logicaDuelo.cpp`:

```cpp
// Apenas o corpo da função, sem necessidade de main() aqui
int atualizaLP(int lpAtual, int dano) {
    return lpAtual - dano;
}
```

Comando de terminal:

```sh
g++ main.cpp logicaDuelo.cpp -o duelo
```

### Exercício 2: Registro de Liga

Arquivo `registroLiga.cpp`:

```cpp
#include <iostream>

int coletaHoras() {
    int horas;
    std::cout << "Digite a quantidade de horas jogadas: ";
    std::cin >> horas;
    return horas;
}
```

Declaração no `main.cpp`:

```cpp
int coletaHoras(); // Deve ser colocado acima da função main
```

Comando de Terminal:

```
g++ *.cpp -o sistemaLiga
```

### Exercício 3:

Comando de Terminal:

```sh
g++ main.cpp ./vetores/*.cpp -o resolveAlgebra
```

## Parte 3: Introdução aos Headers

### Exercício 1: Estruturação de Header e Inclusão

Arquivo `matematica.h`:

```cpp
// Declarações das funções (protótipos)
int calculaFatorial(int num);
int maiorValor(int num1, int num2);
```

Início do arquivo `main.cpp`:

```cpp
#include <iostream>      // Inclui biblioteca padrão usando <>
#include "matematica.h"  // Inclui header do projeto usando ""

int main() {
    // O código segue aqui...
```

### Exercício 3: O Problema das Inclusões Transitivas

Confiar em inclusões transitivas é arriscado por três motivos principais:

1) Quebra de Dependência: Se, no futuro, você decidir remover a necessidade de iostream do arquivo processamento.h, o arquivo processamento.cpp parará de compilar subitamente, mesmo que ele ainda precise de entrada/saída.

2) Clareza e Manutenção: Declarar explicitamente as dependências em cada arquivo torna óbvio para outros programadores (ou para você mesmo no futuro) quais ferramentas aquele arquivo específico utiliza para funcionar.

3) Portabilidade: Diferentes implementações de bibliotecas padrão podem organizar seus próprios headers de forma distinta. O que funciona via "inclusão transitiva" em um compilador pode falhar em outro se a dependência não for explícita.

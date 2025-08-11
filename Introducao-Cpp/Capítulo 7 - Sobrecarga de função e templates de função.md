# Capítulo 7 - Sobrecarga de função e templates de função

Sejam bem-vindos ao Capítulo 7 do nosso curso!

Nesta parte do curso serão abordados temas relacionados a sobrecarga de função e templates de função. 

Em C++, sobrecarga de função, templates de função e o uso adequado de templates em múltiplos arquivos são recursos essenciais para desenvolver código flexível, reutilizável e eficiente.

Esses conceitos são especialmente relevantes em aplicações gráficas com OpenGL, onde a manipulação de dados complexos (como vértices, matrizes e shaders) exige abstrações robustas e desempenho otimizado.

## 7.1 Sobrecarga de função

A sobrecarga de função permite que funções com o mesmo nome tenham comportamentos diferentes, dependendo das configurações (tipo, quantidade ou ordem). 

O compilador escolhe a versão correta com base nos argumentos passados. A sobrecarga **não considera** o tipo de retorno.

Exemplo prático:

```cpp
#include <iostream>
using namespace std;   // permite o uso de elementos da biblioteca padrão sem precisar prefixá-los com "std::"

// Função para somar dois inteiros
int soma(int a, int b) {
    return a + b;
}

// Sobrecarga para somar três inteiros
int soma(int a, int b, int c) {
    return a + b + c;
}

// Sobrecarga para concatenar duas strings
string soma(string a, string b) {
    return a + " " + b;
}

int main() {
    // Chamando a função soma com inteiros
    cout << "Soma de 2 e 3: " << soma(2, 3) << endl; // Saída: 5

    // Chamando a função soma com três inteiros
    cout << "Soma de 2, 3 e 4: " << soma(2, 3, 4) << endl; // Saída: 9

    // Chamando a função soma com strings
    cout << "Concatenando strings: " << soma("Olá", "Mundo") << endl; // Saída: Olá Mundo

    return 0;
}
```
## 7.1 Template de função

Um modelo (template) de função permite criar funções genéricas, capazes de operar com tipos de dados variados, sem precisar reescrevê-las para cada tipo.

Isso é útil para evitar duplicação de código e garantir flexibilidade. 

A definição do template usa a sintaxe `template <typename T>` (ou `template <class T>`), onde `T` é um parâmetro de tipo genérico.

Suponha que você queira uma função que retorne o maior valor entre dois números, seja `int`,`double`,`float`, ou qualquer outro tipo que suporte comparação (>):

```cpp
#include <iostream>
using namespace std;

// Template de função para encontrar o máximo entre dois valores
template <typename T>            // Declaração do template (T é um tipo genérico)
T maximo(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    // Usando com inteiros
    cout << "Máximo entre 10 e 20: " << maximo(10, 20) << endl; // Saída: 20

    // Usando com doubles
    cout << "Máximo entre 3.14 e 2.71: " << maximo(3.14, 2.71) << endl; // Saída: 3.14

    // Usando com caracteres
    cout << "Máximo entre 'a' e 'b': " << maximo('a', 'b') << endl; // Saída: 'b'

    return 0;
}
```

## 7.3 Templates em múltiplos arquivos

Quando você define um modelo (função ou classe), o compilador precisa instanciar versões específicas dele para cada tipo utilizado. 

Para isso, a definição completa do template (implementação) deve estar no cabeçalho (arquivo `.h` ou `.hpp`), pois o código precisa ser "copiado" para cada unidade de compilação que o usa.

O uso de templates no header (cabeçalho) é recomendável quando você precisar reutilizar templates em múltiplos arquivos em projetos grandes e quando desejar evitar duplicação de código para diferentes tipos.

Veja o exemplo a seguir:
```
math_utils.h
```
```cpp
#ifndef MATH_UTILS_H
#define MATH_UTILS_H

// Declaração e definição do template no header
template <typename T>
T Area_quadrado(T x) {
    return x * x;
}

#endif
```
```
main.cpp
```
```cpp
#include <iostream>
#include "math_utils.h"  // Inclui o template

int main() {
    std::cout << "Quadrado de 5: " << Area_quadrado(5) << std::endl;     // Saída: 25
    std::cout << "Quadrado de 3.5: " << Area_quadrado(3.5) << std::endl; // Saída: 12.25
    return 0;
}
```
```
outra_funcao.cpp
```
```cpp
#include "math_utils.h"  // Reutiliza o mesmo template
#include <iostream>

void calcular() {
    std::cout << "Quadrado de 10: " << Area_quadrado(10) << std::endl; // Saída: 100
}
```
Ambos os arquvios `main.cpp` e `outra_funcao.cpp` fazem uso do template que está no header `math_utils.h`

Para compilar basta escrever no terminal:
```
g++ main.cpp outra_funcao.cpp -o meu_programa
```
E para executar:
```
./meu_programa
```

## Questões

1) Função de Soma Genérica com Sobrecarga Específica
- Implemente um template de função somar que soma dois valores de qualquer tipo numérico.
- Depois, crie uma sobrecarga não-template que recebe dois std::string e retorna uma string no formato: "<primeiro> e <segundo>".

Teste com:

```cpp
somar(2, 3)            // 5
somar(2.5, 3.1)        // 5.6
somar("Ana", "João")   // "Ana e João"
```
## Conclusões

Este capítulo abordou sobrecarga de função (funções de mesmo nome com diferentes parâmetros), templates de função (código genérico para múltiplos tipos) e o uso de templates em múltiplos arquivos (definição em cabeçalhos para evitar erros).

Esses recursos permitem código flexível, reutilizável e eficiente, essenciais em aplicações como OpenGL para manipulação de dados complexos.

Te vejo no próximo capítulo :)

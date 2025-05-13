# Capítulo 1 - Parte 5: Introdução a expressões

Agora que você já domina literais e operadores, é hora de combiná‑los em expressões — sequências de valores, variáveis e operadores que produzem um resultado único.

Nesta última parte do capítulo, você verá como construir expressões corretamente, respeitando a precedência e associatividade dos operadores, e como usar parênteses para esclarecer e controlar a ordem de avaliação.

## 5.1 Expressões

Na programação geral, uma expressão é uma sequência não vazia de literais, variáveis, operadores e chamadas de função que calcula um valor.

O processo de execução de uma expressão é chamado de avaliação , e o valor resultante é chamado de resultado da expressão (às vezes também chamado de valor de retorno).

Expressões não terminam em ponto e vírgula e não podem ser compiladas sozinhas. Por exemplo, se você tentasse compilar a expressão x = 5, seu compilador reclamaria (provavelmente sobre a falta de um ponto e vírgula). 

Em vez disso, expressões são sempre avaliadas como parte de instruções.

Por exemplo:
```cpp
int x{ 2 + 3 };       // 2 + 3 é uma expressão que não tem ponto e vírgula - o ponto e vírgula está no final da declaração que contém a expressão
```

## Precedência de Operadores

A precedência de operadores estabelece a hierarquia que determina em que ordem os operadores em uma expressão são avaliados quando não há parênteses explícitos. 

Por exemplo, em 3 + 4 * 5, a multiplicação (*) tem precedência maior que a adição (+).

Veja a seguir uma tabela de precedência de operadores vistos:

| Precedência | Operadores                           | Associatividade       | Descrição                                  |
|-------------|--------------------------------------|-----------------------|--------------------------------------------|
| 1           | `()`                                 | —                     | Agrupamento (força avaliação)              |
| 2           | `!`, `-`, `+`                        | direita para esquerda | Negação lógica, negação aritmética, identidade |
| 3           | `*`, `/`, `%`                        | esquerda para direita | Multiplicação, divisão, resto              |
| 4           | `+`, `-`                             | esquerda para direita | Adição, subtração                          |
| 5           | `<`, `>`, `<=`, `>=`                 | esquerda para direita | Comparações de magnitude                   |
| 6           | `==`, `!=`                           | esquerda para direita | Comparações de igualdade                   |
| 7           | `&&`                                 | esquerda para direita | E lógico                                   |
| 8           | `\|\|`                               | esquerda para direita | OU lógico                                  |
| 9           | `?:` (condicional ternário)          | direita para esquerda | Escolha entre duas expressões              |
| 10          | `=` , `+=`, `-=` , `*=` , `/=` , `%=`| direita para esquerda | Atribuição simples e composta              |

Exemplo de expressões no código:
```cpp
// 1. Multiplicação antes de adição
int r1 = 5 + 3 * 2;        // 5 + (3*2)  = 5 + 6  = 11

// 2. Parênteses alteram a ordem
int r2 = (5 + 3) * 2;      // (5+3) * 2  = 8 * 2  = 16

// 3. Divisão e módulo antes de subtração
int r3 = 20 - 10 / 2;      // 20 - (10/2) = 20 - 5 = 15
int r4 = 20 % 6 + 2;       // (20%6) + 2  = 2 + 2  = 4

// 4. Unários (negação) antes de multiplicação
int x = 3;
int r5 = -x * 4;           // (-x) * 4 = -3 * 4 = -12

// 5. Relacionais antes de lógicos
bool r6 = 5 + 2 > 3 * 2;   // (5+2) > (3*2) → 7 > 6 → true

// 6. Igualdade após relacionais
bool r7 = 5 + 2 == 7;      // (5+2) == 7 → 7 == 7 → true

// 7. Lógicos: AND antes de OR
bool a = true, b = false, c = true;
bool r8 = a && b || c;     // (a&&b) || c → false || true → true

// 8. Ternário após OR
int r9 = a && b || c ? 100 : 200;
//   (a&&b) → false; false||c → true; → r9 = 100
```

## Conclusões

Encerramos aqui nossa jornada do capítulo 1 pelas expressões em C++, onde combinamos literais, variáveis e diversos operadores para produzir valores e tomar decisões. 

Você aprendeu a montar desde operações aritméticas simples até testes lógicos mais elaborados, sempre atento à precedência e associatividade para garantir resultados previsíveis.

No próximo capítulo, será abordado mais sobre os tipos fundamentais de dados e contole de fluxo a partir do uso do `if`.

Aguardo você no capítulo 2!

# Capítulo 1 - Parte 3: Introdução a literais, operadores e expressões

Agora que você já sabe como declarar variáveis e entende a estrutura básica de um programa em C++, é hora de aprender a trabalhar com valores e operações.

Nesta seção, vamos apresentar os literais — valores fixos que você escreve diretamente no código, como `42`, `'A'` ou `"Olá"` — e os operadores, que permitem realizar cálculos, atribuições, comparações e decisões lógicas.

Dominar literais e operadores é essencial para expressar lógica em qualquer programa, desde as operações mais simples até construções mais complexas. Vamos conhecer os principais tipos e como utilizá-los com eficiência!

## 1.6 Literais

Um literal (também conhecido como constante literal) é um valor fixo que foi inserido diretamente no código-fonte. 

Veja o exemplo a seguir:

```cpp
std::cout << "Hello world!";
int x =5;
```
"Hello world!" e "5" são literais. 

## 1.7 Operadores

Em C++, existem diferentes categorias de operadores: aritméticos, de atribuição, de comparação e lógicos. Cada grupo tem uma função específica, como somar números, comparar valores ou tomar decisões com base em condições.

Veja a seguinte tabela com alguns exemplos importantes de operadores: 

| Categoria     | Operadores               | Exemplo             | Descrição                         | Resultado |
|---------------|--------------------------|---------------------|-----------------------------------|-----------|
| Aritméticos   | `+`, `-`, `*`, `/`, `%`  | `5 % 2`             | Resto da divisão inteira          | `1`       |
| Atribuição    | `=`, `+=`, `-=`, `*=`, `/=` | `x = 10; x += 5;`| Soma e atribui ao próprio x       | `x == 15` |
| Comparação    | `==`, `!=`, `<`, `>`, `<=`, `>=` | `5 > 3`     | Compara se 5 é maior que 3        | `true`    |
| Lógicos (E)   | `&&`                     | `true && false`     | Operador “E” lógico               | `false`   |
| Lógicos (OU)  | `\|\|`                   | `true \|\| false`   | Operador “OU” lógico              | `true`    |
| Lógicos (NÃO) | `!`                      | `!true`             | Negação lógica                    | `false`   |

## 1.8 Expressões

Expressões não terminam em ponto e vírgula e não podem ser compiladas sozinhas. Por exemplo, se você tentasse compilar a expressão x = 5, seu compilador reclamaria (provavelmente sobre a falta de um ponto e vírgula). 

Em vez disso, expressões são sempre avaliadas como parte de instruções.

Por exemplo:
```cpp
int x{ 2 + 3 };       // 2 + 3 é uma expressão que não tem ponto e vírgula - o ponto e vírgula está no final da declaração que contém a expressão
```

## 1.9 Precedência de Operadores

A precedência de operadores estabelece a hierarquia que determina em que ordem os operadores em uma expressão são avaliados quando não há parênteses explícitos. 

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
## Questões complementares

1) Escreva uma expressão booleana que seja verdadeira apenas se:
- idade for maior que 18 **e**
- idade for menor ou igual a 30

2) Qual será o valor de x no código abaixo? Explique a ordem de avaliação:

```cpp
int x = (2 + 3) * 4 > 10 && 8 % 3 == 2 ? 100 : 200;
```

3) Crie um programa que:
- Pergunte a nota final (double) e a frequência (int em %) de um aluno.
- Use operadores lógicos para verificar se o aluno está aprovado:
  
Nota maior ou igual a 6.0

Frequência maior ou igual a 75%
- Mostre no console "Aprovado" ou "Reprovado", usando o operador ternário ?:
  
## Conclusões

Encerramos aqui nossa jornada do Capítulo 1 pelas expressões em C++, onde combinamos literais, variáveis e diversos operadores para produzir valores e tomar decisões. 

Você aprendeu a montar desde operações aritméticas simples até testes lógicos mais elaborados, sempre atento à precedência e associatividade para garantir resultados previsíveis.

No próximo capítulo, será abordado mais sobre os tipos fundamentais de dados e controle de fluxo a partir do uso do `if`.

Aguardo você no capítulo 2!

# Capítulo 1 - Parte 4: Introdução a literais e operadores

Agora que você já sabe como declarar variáveis e entende a estrutura básica de um programa em C++, é hora de aprender a trabalhar com valores e operações.

Nesta seção, vamos apresentar os literais — valores fixos que você escreve diretamente no código, como `42`, `'A'` ou `"Olá"` — e os operadores, que permitem realizar cálculos, atribuições, comparações e decisões lógicas.

Dominar literais e operadores é essencial para expressar lógica em qualquer programa, desde as operações mais simples até construções mais complexas. Vamos conhecer os principais tipos e como utilizá-los com eficiência!

## 4.1 Literais

Um literal (também conhecido como constante literal ) é um valor fixo que foi inserido diretamente no código-fonte.

Literais e variáveis ​​têm um valor (e um tipo). Ao contrário de uma variável (cujo valor pode ser definido e alterado por inicialização e atribuição, respectivamente), o valor de um literal é fixo e não pode ser alterado. 

Veja o exemplo a seguir:

```cpp
std::cout << "Hello world!";
int x =5;
```
"Hello world!" e "5" são literais. O literal 5 sempre tem valor 5. É por isso que os literais são chamados de constantes.

## 4.2 Operadores

Os operadores são símbolos especiais usados para realizar operações com variáveis e valores. Eles são fundamentais para escrever expressões, manipular dados e controlar o fluxo do programa.

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

## Conclusões

Nesta seção, você conheceu os literais — valores fixos no código como números, caracteres e strings — e os operadores, que são os símbolos responsáveis por combinar, comparar e manipular esses valores em expressões.

Na próxima parte falaremos sobre expressões, te espero lá!

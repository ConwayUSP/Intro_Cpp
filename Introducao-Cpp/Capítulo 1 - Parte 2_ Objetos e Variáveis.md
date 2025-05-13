# Capítulo 1 - Parte 2: Objetos e Variáveis

Na primeira parte do capítulo 1, nós vimos que funções são grupos de declarações executadas sequencialmente. 

E as declarações dentro da função executam ações que (com sorte) geram o resultado que o programa foi projetado para produzir.

Mas como os programas realmente produzem resultados? Eles o fazem manipulando (lendo, alterando e gravando) dados. 

Então, nessa parte do capítulo veremos como o programa manipula esses dados, a partir de **objetos** e **variáveis**, para alcançar o seu objetivo final.

## 2.1 Objetos

Objetos em C++ são instâncias de tipos, seja um tipo pré-definido pela linguagem (como `int`, `double` ou `std::string`), seja um tipo definido pelo próprio programador (uma classe).

Cada objeto agrupa dados — seus atributos — e pode também agrupar comportamentos — seus métodos. 

Por exemplo, um objeto `Pessoa` pode conter atributos como `nome` e `idade`, e métodos como `falar()` ou `aniversariar()`. Exemplos:

```cpp
int x = 5;                          // Objeto do tipo primitivo
std::string nome = "Alice";         // Objeto de uma classe Pessoa
Pessoa pessoa1;                     // Objeto de classe definida pelo programador
```

## 2.2 Variáveis

Variáveis são nomes associados a locais de memória onde os dados desses objetos são armazenados. 

Declarar uma variável é dizer ao compilador: “reserve espaço para este tipo de dado e associe-o a este identificador”. 

A importância das variáveis está justamente em permitir que o programa armazene, altere e recupere informações ao longo da execução.

Para usá-las, declare seu tipo e nome:

```cpp
int idade;          // Declara uma variável inteira chamada 'idade'
idade = 25;         // Atribui o valor 25 à variável através do operador de atribuição "="

double preco = 9.99; // Declara e inicializa em uma única linha
```

> Um dos erros mais comuns é confundir o operador de atribuição ( = ) com o operador de igualdade ( == ).
> 
> Atribuição ( = ) é usada para atribuir um valor a uma variável. Igualdade ( == ) é usada para testar se dois operandos têm o mesmo valor.

### Exemplos de Tipos de Dados Comuns:

| Tipo     | Descrição                    | Exemplo     | Tamanho (bytes) |
| -------- | ---------------------------- | ----------- | --------------- |
| `int`    | Números inteiros             | 42, -7      | 4               |
| `double` | Números decimais             | 3.14, -0.5  | 8               |
| `char`   | Caractere único              | 'A', '\$'   | 1               |
| `bool`   | Valores lógicos              | true, false | 1               |

Outra declaração aceita para tipos de dados é unir as palavras reservadas signed e unsigned ao tipo, declarações que aceitam valores com representação negativa **(signed)** ou tipos que não aceitam valores negativos **(unsigned)**.

Recomendamos procurar mais sobre outros tipos de dados para se apronfundar e ter maior repertório!

## Conclusão

Neste capítulo, aprendemos que  vimos que objetos em C++ representam instâncias concretas de tipos — sejam tipos primitivos como `int` e `double`, ou tipos definidos pelo programador via `class` — e que cada objeto ocupa um espaço de memória onde seus atributos são armazenados.

Já as variáveis são simplesmente nomes associados a esses locais de memória, permitindo que seu programa armazene, modifique e recupere valores ao longo da execução.

Até breve!

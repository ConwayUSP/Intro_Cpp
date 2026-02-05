# Capítulo 2 - Parte 2: Trabalhando com os Tipos de Dados
Na segunda parte do Capítulo 2, vamos nos aprofundar nos tipos de dados que aprendemos brevemente. Conheceremos um pouco dos inteiros com e sem sinal (signed/unsigned), números de ponto flutuante, tipo bool e os comandos if e else, e alguns outros conceitos! Vamos lá?

## 2.7 - Números Inteiros com Sinal (Signed Integers)

Um inteiro (`int`) é um tipo que pode representar números positivos e negativos, incluindo 0. Como vimos anteriormente, o C++ tem tem 4 tipos de inteiro disponíveis para uso: `short int`, `int`, `long int` e `long long int`. A diferença entre estes vários tipos de inteiro é o tamanho que eles ocupam, sendo os maiores os que conseguem armazenar maiores números (como o `long long int`, por exemplo).

|Tipo|Tamanho Mínimo|
|----|--------------|
|short int|16 bits|
|int| 16 bits|
|long int| 32 bits|
|long long int|64 bits|
>**Observação:** `int` geralmente tem tamanho mínimo de 32 bits em arquiteturas modernas.

Aqui está a maneira preferível de definir os 4 tipos de inteiros:

```cpp
short s;      // escreva "short" ao invès de "short int"
int i;
long l;       // escreva "long" ao invés de "long int"
long long ll; // escreva "long long" ao invés de "long long int"
```
Mesmo que escrever da forma longa funcione (como por exemplo escrever: `short int s;`), é melhor escrever a forma curta pois é mais fácil de escrever e também ajuda a distinguir as variáveis do tipo `int`.

Quando escrevemos um número negativo na vida real, colocamos um sinal negativo na frente do número (como por exemplo: -3). Se colocássemos o sinal positivo na frente de um número (como por exemplo: +3), também compreenderíamos, mesmo que a convenção comum seja de omitir o sinal positivo. Portanto, o atributo de ser positivo, negativo ou zero é chamado de **sinal** de um número (ou **sign**, em inglês)

Por padrão, inteiros em C++ têm sinal (ou **signed**, em inglês), o que significa que o sinal de um número é armazenado junto com o valor em si. Então, um inteiro com sinal pode guardar tanto positivos, negativos e o zero.

Por isso, podemos definir nossos inteiros com um modificador `signed` adicional, que por convenção é colocado antes do nome do tipo:
```cpp
signed short ss;
signed int si;
signed long sl;
signed long long sll;
```
No entando, esse modificador não deve ser usado pois é redundante, já que os inteiros já são `signed` (com sinal) por padrão.

O C++ também possui inteiros **sem sinal** (ou **unsigned**, em inglês), que são inteiros que só podem ser números não-negativos. Definimos os inteiros sem sinal de forma semelhante ao `signed`, porém substituindo pelo modificador `unsigned`:
```cpp
unsigned short us;
unsigned int ui;
unsigned long ul;
unsigned long long ull;
```
De forma geral programadores mais experientes recomendam evitar o uso do modificador `unsigned`, já que muitas vezes podemos manipular os números de forma equivada, causando um overflow no nosso código. Para dar um exemplo, com muita frequência iteramos em loops subtraindo uma variável repetidamente por 1, se nossa variável for não-negativa e o código tentar subtrai-la para um número negativo, isso causará problemas! Também podem acontecer comportamentos inesperados se tentarmos misturar o uso de números `signed` e `unsigned`, então use com grande cuidado, sabedoria e apenas quando necessário!

## 2.8 - Números de Ponto Flutuante

Inteiros são muito bons para contar números, mas as vezes precisamos guardar números **realmente** grandes, ou números decimais. Uma váriavel de  tipo **ponto flutuante** é uma variável que consegue armazenar um número decimal, como 25.33, 34445.0, -50.2 e assim em diante. A parte flutuante se refere ao fato de que o ponto decimal pode "flutuar", isto é, ele abarca um número variável de dígitos antes e depois do ponto decimal. Os tipos de dado de ponto flutuante são sempre `signed`. 

O C++ tem três tipos de dado de ponto flutuante disponíveis para uso: `float`, `double` e `long double`. Novamente, a diferença entre eles é o tamanho da memória que ocupam, sendo os tipos maiores mais precisos (isto é, oferecem mais dígitos decimais).
|Tipo|Tamanho Típico|
|----|--------------|
|float|4 bytes|
|double|8 bytes|
|long double| 8, 12 ou 16 bytes|

Para definir os tipos de ponto flutuante, usamos:
```cpp
float f;
double d;
long double ld;
```
Quando estiver usando literais de ponto flutuante, inclua pelo menos um espaço de decimal (mesmo que seja 0). Isso ajuda o compilador a entender que o número é um tipo de ponto flutuante e não um inteiro. Por padrão, os literais de ponto flutuante são interpretados como `double`, e usamos um sufixo `f` para denotar que um literal é do tipo `float`. Vejamos:
```cpp
int a { 5 };      // 5 significa inteiro
double b { 5.0 }; // 5.0 é um literal de ponto flutuante (sem sufixo significa double por padrão)
float c { 5.0f }; // 5.0 é um literal de ponto flutuantel, o sufixo f significa tipo float

int d { 0 };      // 0 é um inteiro
double e { 0.0 }; // 0.0 é um double
```
>**Observação:** Lembre-se de sempre verificar se os literais se adequam as variáveis que eles estão sendo atribuídos, pois senão uma conversão desnecessária será realizada, o que pode ocasionar em perda de precisão.

## 2.9 - Valores Booleanos
Variáveis booleanas são mais simples, e possuem apenas dois valores possíveis, sendo eles: `true` ou `false` (verdadeiro ou falso). Estes valores são armazenados como valores inteiros 1 (para `true`) e 0 (para `false`), por isso fazem parte da categoria de tipos inteiros. 

Para declarar uma variável booleana, usamos o termo `bool`.
```cpp
bool b;
```
E para inicializar ou atribuir algum dos dois valores possíveis à uma variável, fazemos da seguinte forma: 
```cpp
bool b1 { true };
bool b2 { false };
b1 = false;
bool b3 {}; // inicializa como false por padrão
```
Pode-se também utilizar o operador lógico NOT (!) para tornar um valor `true` para `false`, e vice-versa.
```cpp
bool b1 { !true }; // b1 inicializa como false
bool b2 { !false }; // b2 inicializa como true
```
Com muita frequência usamos valores booleanos como os valores de retorno para funções que checam se algo é verdadeiro ou não. Estas funções geralmente são nomeadas começando pelas palavras **é** ou **tem**, na maioria das vezes escritas em inglês **is** e **has**, como por exemplo nas funções `isEqual()` ou `hasCommonDivisor`.  

## 2.10 - Introdução aos comandos if e if-else
Se você já estudou um pouco de C, também já deve estar familiarizado com a condicional `if` (ou **"se"**, traduzindo do inglês), que nos permite executar linhas de código caso alguma condição seja verdadeira. Uma **condição** (também chamada de **expressão condicional**) é uma expressão que verifica um valor booleano, elas são escritas a partir dos operadores lógicos e de comparação que estudamos no capítulo anterior (ex. expressão condicional: 1 == 2, resultado: false). Se esse valor for `true`, então o pedaço de código é executado, caso contrário, aquele pedaço de código é ignorado.  

Aqui está um pequeno exemplo do uso de if:
```cpp
#include <iostream>

int main()
{
    std::cout << "Escreva um inteiro: ";
    int x {};
    std::cin >> x;

    if (x == 0)
        std::cout << "O valor é zero\n";

    return 0;
}
```
Podemos incluir também o comando `else` após o `if`, produzindo o comando `if-else`. Basicamente, `if-else` implica que se a expressão condicional definida no `if` resultar em um valor negativo (como em: `if (1 == 2)`, então deve-se ignorar o pedaço de código no escopo do `if` e executar o pedaço de código alternativo definido no escopo do `else` (entenda como: "se não isto, então aquilo").

Aqui está um pequeno exemplo do uso de if-else:
```cpp
#include <iostream>

int main()
{
    std::cout << "Escreva um inteiro: ";
    int x {};
    std::cin >> x;

    if (x == 0)
        std::cout << "O valor é zero\n";
    else
        std::cout << "O valor não é zero\n";

    return 0;
}
```

## 2.11 - Chars
Até agora olhamos apenas para os tipos que armazenam números ou valores como `true`/`false`, mas e se quisermos armazenar letras? Utilizamos o tipo de dado chamado `char`, que consegue armazenar **apenas um** caractere, que pode ser uma letra, um número, um símbolo ou um espaço em branco. Como já explicamos, este tipo é armazenado como um número inteiro, porém neste caso o valor é interpretado através de uma tabela que traduz os números para caracteres.
>**Observação:** Há vários padrões de tabela bastante utilizados ao redor do mundo, como **ASCII** e **UTF-8**, porém abordaremos em detalhes neste curso. Caso tenha ficado curioso, recomendo a pesquisa!

Para definir um char, utilizamos:
```cpp
char ch2{ 'a' }; //lembre-se de usar as aspas!
```
Também há algumas sequências de caracteres em C++ que têm um significado especial, essas sequências são chamadas de **sequências de escape**, que começam com um caractere de barra invertida `'\'`, e então um número ou letra. Provavelmente você já conhece a sequência mais comum: `'\n'`, que pode ser usada para fazer impressões em uma nova linha. 

Aqui está uma lista das sequências de escape:

| Nome | Símbolo | Significado |
|------|---------|-------------|
| **Alerta** | `\a` | Emite um alerta, como um bipe |
| **Backspace** | `\b` | Move o cursor uma posição para trás |
| **Formfeed** | `\f` | Move o cursor para a próxima página lógica |
| **Nova linha** | `\n` | Move o cursor para a próxima linha |
| **Retorno de carro** | `\r` | Move o cursor para o início da linha |
| **Tabulação horizontal** | `\t` | Imprime uma tabulação horizontal |
| **Tabulação vertical** | `\v` | Imprime uma tabulação vertical |
| **Aspas simples** | `\'` | Imprime uma aspas simples |
| **Aspas duplas** | `\"` | Imprime aspas duplas |
| **Barra invertida** | `\\` | Imprime uma barra invertida |
| **Ponto de interrogação** | `\?` | Imprime um ponto de interrogação |
| **Número octal** | `\(número)` | Traduz para o caractere representado pelo número octal |
| **Número hexadecimal** | `\x(número)` | Traduz para o caractere representado pelo número hexadecimal |

>**Observação:** O escape `\?` **não é mais relevante** na maioria dos casos. Você pode usar pontos de interrogação sem escape em C++ moderno. E para `\(número)` e `\x(número)`, substitua `(número)` pelo valor real (ex: `\101` para octal 'A', `\x41` para hexadecimal 'A').

## 2.12 - Conversão de Tipos e o static_cast

Vejamos um exemplo:
```cpp
#include <iostream>

void imprime(double x) // imprime() recebe um double
{
	std::cout << x << '\n';
}

int main()
{
	imprime(5); // o que acontece se passarmos um valor do tipo int?

	return 0;
}
```
Na maioria dos casos, o C++ permite a conversão entre valores de um tipo fundamental para outro tipo fundamental, este processo é chamado de **conversão de tipo**. No exemplo acima, o valor inteiro `5` será convertido para o valor double `5.0`, e então copiado como parâmetro para a função `imprime()`. Como foi o compilador que realizou esta conversão no nosso lugar, o que aconteceu foi uma **conversão implícita de tipo**, que muitas vezes funciona, porém precisamos tomar cuidado. Vejamos:
```cpp
#include <iostream>

void imprime(int x) // imprime() agora recebe um int como parâmetro
{
	std::cout << x << '\n';
}

int main()
{
	imprime(5.5); // cuidado! estamos passando um valor double como parâmetro

	return 0;
}
```
Neste caso, provavelmente seu compilador gerará algum aviso de perda de dados ou até abortará a execução do programa, então tenha cuidado!

No entando, muitas vezes queremos que a conversão aconteça mesmo que ocorra perda de dados, e é nesses momentos que utlizamos a **conversão explícita de tipo**. Essa conversão nos permite dizer explicitamente ao compilador para converter um valor de um tipo para outro, e que assumimos a responsabilidade dos resultados desta conversão.
Para realizar  uma conversão de tipo explícita, utilizamos geralmente o operador `static_cast`, cuja sintaxe é a seguinte:
```cpp
static_cast<novo_tipo>(expressão)
```
O `static_cast` recebe o valor de uma expressão como entrada e retorna o valor convertido no tipo especificado em `<novo_tipo>` (ex. `int`, `bool`, `char`, `double`).
Vejamos como nosso código anterior ficaria:
```cpp
#include <iostream>

void imprime(int x)
{
	std::cout << x << '\n';
}

int main()
{
	imprime( static_cast<int>(5.5) ); // converte explicitamente o valor double 5.5 em um int

	return 0;
}
```
# Conclusões
Agora sim saímos deste capítulo com um montão de possibilidades! Na próxima etapa, expandiremos ainda mais seus conhecimentos em C++, estudando funções, headers e muito mais. Te encontro lá!

# Capítulo 2 - Parte 2: 

Neste parte, conheceremos... (continuar)

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

## 2.10 - Introdução ao comando if



# Conclusões

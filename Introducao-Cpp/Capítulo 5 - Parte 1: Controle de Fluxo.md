# Capítulo 5 - Parte 1: Controle de Fluxo

## 5.1 - Introdução ao Controle de Fluxo

Aprendemos que a CPU do nosso computador inicia a execução pelo topo da função `main()`, executa as instruções do nosso código em ordem sequencial, e então termina no fim da função `main()`. Chamamos esta sequência que a CPU percorre de **caminho de execução** (ou apenas **caminho**).

Vejamos este exemplo:
```cpp
#include <iostream>

int main()
{
    std::cout << "Digite um inteiro: ";

    int x{};
    std::cin >> x;

    std::cout << "Você digitou " << x << '\n';

    return 0;
}
```

O caminho deste programa segue a ordem das linhas (1, 2, 3 e assim em diante) até o fim de sua execução. Este é um exemplo de **programa de linha reta**, que são programas que executam a mesma ordem toda vez que o executamos.

Mas nem sempre é isso que queremos! Se pedirmos uma entrada para um usuário e este usuário digitar algo inválido, seria melhor pedir para o usuário digitar alguma outra coisa, certo? Porém isto não é possível com proramas de linha reta!

Para mudar isso, o C++ nos fornece diferentes declarações de **controle de fluxo**, que nos permitem mudar o caminho normal de execução durante o programa. Já vimos um pouco disso durante o capítulo 2, introduzindo o `if` e `if-else`. Veremos agora algumas declarações novas, aqui está uma tabela com as diferentes categorias de instruções de controle de fluxo:

**Categoria** | **Significado** | **Implementado em C++ usando**
--- | --- | ---
Declarações condicionais | Faz com que uma sequência de código seja executada apenas se alguma condição for atendida. | `if`, `else`, `switch`
Saltos (Jumps) | Instrui a CPU a começar a executar as instruções em algum outro local. | `goto`, `break`, `continue`
Chamadas de função | Salta para outro local e retorna. | chamadas de função, `return`
Laços (Loops) | Executa repetidamente uma sequência de código zero ou mais vezes, até que uma condição seja atendida. | `while`, `do-while`, `for`, ranged-for (`for` baseado em intervalo)
Interrupções (Halts) | Termina o programa. | `std::exit()`, `std::abort()`
Exceções | Um tipo especial de estrutura de controle de fluxo projetada para tratamento de erros. | `try`, `throw`, `catch`

## 5.2 - Declarações Condicionais

### Blocos Implícitos

No capítulo 2, quando estudamos as declarações condicionais, não comentamos sobre blocos. Então aqui vai uma breve explicação! **Blocos** são um pedaço da declaração de um `if` ou `else`, que se não declarados, o compilador implicitamente declara para nós. Um **bloco** então é um grupo de declarações (instruções) tratadas como uma unidade pelo compilador. Em C++ e muitas outras linguagens, um bloco é delimitado por chaves `{ }`. Veja:
```cpp
if (condicao)
    declaracao_verdadeira;
else
    declaracao_falsa;
```
É equivalente a:
```cpp
if (condicao)
{
    declaracao_verdadeira;
}
else
{
    declaracao_falsa;
}
```
Há um debate grande no mundo dos programadores em se devemos ou não declarar explicitamente os blocos, porém para iniciantes recomenda-se usá-los para evitar erros sutis e tornar o código mais legível, mesmo que o código fique menos conciso.

### Declarações Nulas

Uma **declaração nula** (null statement) é uma expressão que consiste em apenas um **ponto e virgula**:
```cpp
if (x > 10)
    ; // esta é uma declaração nula
```
Declarações nulas não fazem nada e são tipicamente usadas quando a linguagem exige que uma declaração exista mas o programador não precisa de uma. Sabendo disso, devemos tomar cuidado pois se acidentalmente digitarmos um `;` no meio do nosso código, o código compila normalmente e podem ocorrer erros inesperados!

### Declarações Constexpr if

Normalmente as condicionais de um `if` são verificadas em tempo de execução de um programa. Porém, se uma condicional for uma **expressão constante**, isto é, uma expressão que **sempre** será avaliada como verdadeira (ou falsa, a depender da expressão), avaliar esta condicional em tempo de execução é uma perda de tempo, já que o resultado nunca irá mudar. Para isso o C++ introduz a declaração `constexpr if` que necessita que a condicional seja uma expressão constante. A condicional de um `constexpr if` é verificada em tempo de compilação, economizando recursos computacionais.

Vejamos:
```cpp
#include <iostream>

int main()
{
	constexpr double gravidade{ 9.8 }; // a gravidade sempre terá um valor constante

	if constexpr (gravidade == 9.8) // agora usando contexpr if, pois a condicional sempre será verdadeira
		std::cout << "A gravidade está normal.\n";
	else
		std::cout << "Não estamos no planeta terra.\n";

	return 0;
}
```
Na prática, o compilador verá que a a condicional sempre será `true`, e manterá apenas o seguinte:
```cpp
int main()
{
	constexpr double gravidade{ 9.8 };

	std::cout << "A gravidade está normal.\n";

	return 0;
}
```
Recomenda-se usar `constexpr if` sempre que estiver trabalhando com condicinais que são constantes.

### Declaração Switch

Mesmo que seja possível declarar vários `if-else` em sequência, fazer desta forma é difícil de ler e acaba sendo ineficiente. Vejamos:
```cpp
#include <iostream>

void imprimeDigito(int x)
{
    if (x == 1)
        std::cout << "Um";
    else if (x == 2)
        std::cout << "Dois";
    else if (x == 3)
        std::cout << "Três";
    else
        std::cout << "Dígito Desconhecido";
}

int main()
{
    imprimeDígito(2);
    std::cout << '\n';

    return 0;
}
```
Neste código, a variável `x` na função `imprimeDigito()` será verificada até três vezes dependendo do valor que passarmos a ela. Tendo em vista que é muito comum testar se uma variável é equivalente à um grupo diferente de valores, o C++ nos fornece uma declaração condicional alternativa chamada de `switch`, especializada para este propósito. Aqui está o mesmo programa anterior, porém usando `switch`:
```cpp
#include <iostream>

void imprimeDigito(int x)
{
    switch (x)
    {
    case 1:
        std::cout << "Um";
        return;
    case 2:
        std::cout << "Dois";
        return;
    case 3:
        std::cout << "Três";
        return;
    default:
        std::cout << "Dígito Desconhecido";
        return;
    }
}

int main()
{
    imprimeDigito(2);
    std::cout << '\n';

    return 0;
}
```

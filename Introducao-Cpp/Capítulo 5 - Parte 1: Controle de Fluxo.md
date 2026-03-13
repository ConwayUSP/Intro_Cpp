# Capítulo 5 - Parte 1: Controle de Fluxo

Sejam bem-vindos à primeira parte do Capítulo 5 da nossa trilha!

Até agora, nossos programas seguiam um caminho previsível: início, execução linha a linha, fim. Mas e quando precisamos tomar decisões? E se quisermos que o programa reaja de forma diferente dependendo da entrada do usuário? É exatamente isso que vamos começar a explorar agora!

Nesta primeira parte, vamos mergulhar no universo do controle de fluxo condicional. Prepare-se para dar os primeiros passos além da linha reta!

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

## 5.2 - Tópicos Especiais sobre if

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

## 5.3 - Declaração Switch

Mesmo que seja possível declarar vários `if-else` em sequência, fazer isso torna o código difícil de ler e em alguns casos acaba sendo ineficiente. Vejamos:
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
Portanto, a ideia por traz de uma declaração `switch` é bem simples: uma expressão (também chamada de condição) é avaliada para produzir um valor. Nesse sentido, sempre ocorrerá uma entre três destas possibilidades:
- Se o valor da expressão for equivalente ao valor de algum dos casos, o bloco de código daquele caso é executado;
- Se o valor da expressão não for equivalente a nenhum caso e um rótulo padrão existir, o bloco de código do rótulo padrão é executado;
- Se o valor da expressão não for equivalente a nenhum caso e não há rótulo padrão, ignora-se o `switch`.

Recomenda-se usar a declaração `switch` quando há apenas uma expressão (com um valor não-booleano inteiro ou um tipo enumerável) que queremos comparar com um grupo de números para encontrar equivalência.

Até agora usamos a declaração `return` para terminar a execução das instruções após o rótulo, porém esta forma fará com que a função toda termine. Caso queiramos que nossa função continue executando após o `switch`, devemos usar a declaração `break`, que diz ao compilador que terminamos de executar as instruções dentro do switch, e que deve-se continuar a execução a partir do fim do bloco. Vejamos agora o programa anterior, porém usando o `break` ao invès de `return`:

```cpp
#include <iostream>

void imprimeDigito(int x)
{
    switch (x) // x armazena o valor 3
    {
    case 1:
        std::cout << "Um";
        break;
    case 2:
        std::cout << "Dois";
        break;
    case 3:
        std::cout << "Três"; // a execução começa aqui
        break; // pula para o fim do bloco switch
    default:
        std::cout << "Dígito Desconhecido";
        break;
    }

    // a execução continua aqui
    std::cout << " Ah-Ah-Ah!";
}

int main()
{
    imprimeDigito(3);
    std::cout << '\n';

    return 0;
}
```

### Cascata (Fallthrough)

Quando uma expressão `switch` corresponde a um rótulo `case` ou ao rótulo opcional `default`, a execução começa na primeira instrução após o rótulo correspondente. A execução então continua sequencialmente até que uma das seguintes condições de término aconteça:

-    O final do bloco `switch` seja alcançado.

-   Outra instrução de controle de fluxo (geralmente `break` ou `return`) faça com que o bloco `switch` ou a função termine.

-  Algo mais interrompa o fluxo normal do programa (por exemplo, o sistema operacional finalize o programa, o universo imploda, etc.).

Observe que a presença de outro rótulo case não é uma dessas condições de término – portanto, sem um `break` ou `return`, a execução continuará para os casos subsequentes. Esse comportamento é chamado de cascata (fallthrough).

Aqui está um programa que exibe esse comportamento:
```cpp
#include <iostream>

int main()
{
    switch (2)
    {
    case 1: // Não corresponde
        std::cout << 1 << '\n'; // Ignorado
    case 2: // Correspondeu!
        std::cout << 2 << '\n'; // A execução começa aqui
    case 3:
        std::cout << 3 << '\n'; // Isto também é executado
    case 4:
        std::cout << 4 << '\n'; // Isto também é executado
    default:
        std::cout << 5 << '\n'; // Isto também é executado
    }

    return 0;
}
```

Este programa produz a seguinte saída:
```text
2
3
4
5
```
Provavelmente não era isso que queríamos! Quando a execução flui das instruções de um rótulo para as instruções de um rótulo seguinte, chamamos isso de cascata (fallthrough). Como a cascata raramente é desejada ou intencional, muitos compiladores e ferramentas de análise de código sinalizarão a cascata como um aviso (warning).

## Questões

# Conclusões

Chegamos ao final da primeira parte do Capítulo 5!

Agora você descobriu muitos recursos novos úteis para nós programadores! Mas isso é só o começo! Na segunda parte deste capítulo, vamos dar um passo além e aprender a repetir ações com os laços (loops), além de conhecer as instruções goto, break e continue.

Te espero lá!


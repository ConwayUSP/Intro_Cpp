# Capítulo 5 - Parte 2: Continuação de Controle de Fluxo

Olá novamente! Na segunda parte do Capítulo 5, você vai conhecer mais algumas ferramentas importantes para manipular o fluxo de execução do nosso código!

Vamos lá?

## 5.5 – Declaração Goto

O próximo tipo de declaração de controle de fluxo que veremos é o **salto incondicional**. Um salto incondicional faz com que a execução salte para outro ponto do código. O termo "incondicional" significa que o salto sempre acontece (diferente de um `if` ou `switch`, onde o salto ocorre apenas condicionalmente com base no resultado de uma expressão).

Em C++, saltos incondicionais são implementados via declaração `goto`, e o ponto para o qual saltamos é identificado por um **rótulo de declaração** (statement label). Assim como os rótulos `case` do `switch`, os rótulos de declaração convencionalmente não são indentados.

Aqui está um exemplo de uso do `goto`:

```cpp
#include <iostream>
#include <cmath> // para a função sqrt()

int main()
{
    double x{};
tentarNovamente: // este é um rótulo de declaração
    std::cout << "Digite um número não negativo: ";
    std::cin >> x;

    if (x < 0.0)
        goto tentarNovamente; // esta é a declaração goto

    std::cout << "A raiz quadrada de " << x << " é " << std::sqrt(x) << '\n';
    return 0;
}
```

Neste programa, o usuário deve digitar um número não negativo. Se um número negativo for inserido, o programa usa `goto` para saltar de volta ao rótulo `tentarNovamente`. O usuário é então solicitado novamente a digitar um novo número. Desta forma, podemos pedir continuamente a entrada do usuário até que ele digite algo válido.

Exemplo de execução:

```
Digite um número não negativo: -4
Digite um número não negativo: 4
A raiz quadrada de 4 é 2
```

### Limitações dos saltos

Há duas limitações principais para saltos com `goto`:

1. Você só pode saltar dentro dos limites de uma única função (não é possível sair de uma função e entrar em outra).
2. Se você saltar para frente, não pode pular a **inicialização** de qualquer variável que ainda esteja em escopo no ponto de destino. Por exemplo:

```cpp
int main()
{
    goto pular;   // erro: este salto é ilegal porque...
    int x { 5 }; // esta variável inicializada ainda está em escopo no rótulo 'pular'
pular:
    x += 3;      // o que isso avaliaria se x não fosse inicializado?
    return 0;
}
```

Observe que você pode saltar para trás sobre uma inicialização de variável – nesse caso, a variável será reinicializada quando a inicialização for executada novamente.

### Evite usar goto

O uso de `goto` é desaconselhado em C++ (e em outras linguagens modernas de alto nível). O principal problema com `goto` é que ele permite que o programador salte arbitrariamente pelo código, criando o que é conhecido como **código espaguete** – um caminho de execução tão embaralhado quanto um prato de espaguete, tornando extremamente difícil seguir a lógica do programa.

Quase qualquer código escrito com `goto` pode ser reescrito de forma mais clara usando outras construções do C++, como `if` e loops. Uma exceção notável ocorre quando você precisa sair de um loop aninhado, mas não da função inteira – nesse caso, um `goto` para logo após os loops pode ser a solução mais limpa.


## 5.6 – Introdução aos Laços (Loops)

E agora a diversão realmente começa, abordaremos os **laços** (loops). Laços são construções de controle de fluxo que permitem que um pedaço de código seja executado repetidamente até que alguma condição seja atendida.

Por exemplo, digamos que você queira imprimir todos os números entre 1 e 10. Sem laços, você poderia tentar algo assim:

```cpp
#include <iostream>

int main()
{
    std::cout << "1 2 3 4 5 6 7 8 9 10";
    std::cout << " pronto!\n";
    return 0;
}
```

Embora isso seja viável, torna-se cada vez menos à medida que você deseja imprimir mais números: e se você quisesse imprimir todos os números entre 1 e 1000? Seria bastante digitação! Mas um programa assim é escrevível dessa maneira porque sabemos em tempo de compilação quantos números queremos imprimir.

Agora, vamos mudar um pouco os parâmetros. E se quiséssemos pedir ao usuário para digitar um número e então imprimir todos os números entre 1 e o número que o usuário digitou? O número que o usuário digitar não é conhecível em tempo de compilação. Então, como poderíamos resolver isso?

## 5.7 – Declaração while

A instrução `while` (também chamada de **laço while**) é a mais simples dos três tipos de laços que o C++ oferece, e tem uma definição muito semelhante à de uma instrução `if`:

```cpp
while (condicao)
    instrucao;
```

Uma instrução `while` é declarada usando a palavra-chave `while`. Quando uma instrução `while` é executada, a expressão `condicao` é avaliada. Se a condição for avaliada como `true`, a instrução associada é executada.

No entanto, diferentemente de uma instrução `if`, assim que a instrução termina de ser executada, o controle retorna ao topo da instrução `while` e o processo se repete. Isso significa que uma instrução `while` continuará em loop enquanto a condição continuar sendo avaliada como `true`.

Vamos dar uma olhada em um laço `while` simples que imprime todos os números de 1 a 10:

```cpp
#include <iostream>

int main()
{
    int contador{ 1 };
    while (contador <= 10)
    {
        std::cout << contador << ' ';
        ++contador;
    }

    std::cout << "pronto!\n";

    return 0;
}
```

Isso produz:

```
1 2 3 4 5 6 7 8 9 10 pronto!
```

Observe que, se a condição for inicialmente avaliada como falsa, a instrução associada não será executada. Considere o seguinte programa:

Por outro lado, se a expressão sempre for avaliada como verdadeira, o laço `while` executará para sempre. Isso é chamado de **laço infinito**. De vez em quando queremos que isso seja intencional, mas devemos prestar atenção para que funcione de acordo como desejamos! Cada vez que um laço executa, é chamado de **iteração**.

## 5.8 – Declaração do-while

Considere o caso em que queremos mostrar um menu ao usuário e pedir que ele faça uma seleção – e se o usuário escolher uma opção inválida, pedir novamente. Claramente, o menu e a seleção devem estar dentro de algum tipo de laço (para que possamos continuar perguntando até que o usuário forneça uma entrada válida), mas que tipo de laço devemos escolher?

### Declaração do-while

Para ajudar a resolver problemas como o acima, o C++ oferece a instrução **do-while**:

```cpp
do
    instrucao; // pode ser uma única instrução ou um bloco
while (condicao);
```

Uma instrução `do-while` é uma construção de repetição que funciona exatamente como um laço `while`, exceto que a instrução **sempre executa pelo menos uma vez**. Após a execução da instrução, o laço `do-while` verifica a condição. Se a condição for avaliada como verdadeira, o caminho de execução salta de volta para o topo do laço `do-while` e o executa novamente.

Aqui está um exemplo usando um laço `do-while`:

```cpp
#include <iostream>

int main()
{
    // selecao deve ser declarada fora do do-while, para que possamos usá-la depois
    int selecao {};

    do
    {
        std::cout << "Por favor, faça uma seleção: \n";
        std::cout << "1) Adição\n";
        std::cout << "2) Subtração\n";
        std::cout << "3) Multiplicação\n";
        std::cout << "4) Divisão\n";
        std::cin >> selecao;
    }
    while (selecao < 1 || selecao > 4);

    // faz algo com a seleção aqui
    // como uma instrução switch

    std::cout << "Você selecionou a opção #" << selecao << '\n';

    return 0;
}
```

Desta forma, evitamos tanto números mágicos quanto variáveis adicionais.

Um ponto que vale a pena discutir no exemplo acima é que a variável `selecao` deve ser declarada **fora** do bloco `do`. Se a variável `selecao` fosse declarada dentro do bloco `do`, ela seria destruída quando o bloco `do` terminasse, o que acontece **antes** da condição ser avaliada. Mas precisamos da variável na condição do `while` – consequentemente, a variável `selecao` deve ser declarada fora do bloco `do` (mesmo que não seja usada posteriormente no corpo da função).

Na prática, laços `do-while` não são comumente usados. Ter a condição na parte inferior do laço obscurece a condição do laço, o que pode levar a erros. Muitos desenvolvedores recomendam evitar completamente laços `do-while` como resultado. Adotaremos uma postura mais suave e defenderemos a preferência por laços `while` em vez de `do-while` quando houver escolha equivalente.

## 5.9 – Declaração for

A instrução de laço mais utilizada em C++ é a instrução `for` (também chamada de **laço for**). O `for` é preferido quando temos uma variável de laço óbvia, porque nos permite definir, inicializar, testar e alterar o valor de variáveis de laço de forma fácil e concisa.

A sintaxe do `for` parece bastante simples em abstrato:

```cpp
for (instrucao-inicializacao; condicao; expressao-final)
    instrucao;
```

A maneira mais fácil de entender como um `for` funciona é convertê-lo em um `while` equivalente:

```cpp
{ // observe o bloco aqui
    instrucao-inicializacao; // usado para definir variáveis usadas no laço
    while (condicao)
    {
        instrucao;
        expressao-final; // usado para modificar a variável de laço antes de reavaliar a condição
    }
} // as variáveis definidas dentro do laço saem de escopo aqui
```

### Avaliação de instruções for

Uma instrução `for` é avaliada em 3 partes:

1. Primeiro, a **instrução-inicialização** é executada. Isso acontece apenas uma vez, quando o laço é iniciado. A instrução-inicialização é tipicamente usada para definição e inicialização de variáveis. Essas variáveis têm "escopo de laço", que é na verdade uma forma de escopo de bloco onde essas variáveis existem desde o ponto de definição até o final da instrução do laço. No equivalente com `while`, você pode ver que a instrução-inicialização está dentro de um bloco que contém o laço, então as variáveis definidas na instrução-inicialização saem de escopo quando o bloco que contém o laço termina.

2. Em segundo lugar, a cada iteração do laço, a **condição** é avaliada. Se for avaliada como `true`, a instrução é executada. Se for `false`, o laço termina e a execução continua com a próxima instrução após o laço.

3. Finalmente, após a instrução ser executada, a **expressão-final** é avaliada. Tipicamente, essa expressão é usada para incrementar ou decrementar as variáveis de laço definidas na instrução-inicialização. Depois que a expressão-final é avaliada, a execução retorna ao segundo passo (e a condição é avaliada novamente).

> **Visão importante**
>
> A ordem de execução das diferentes partes de uma instrução `for` é a seguinte:
>
> 1. Instrução-inicialização
> 2. Condição (se for falsa, o laço termina aqui)
> 3. Corpo do laço
> 4. Expressão-final (então volta para a condição)

Observe que a expressão-final é executada **após** a instrução do laço, e então a condição é reavaliada.

Vamos dar uma olhada em um exemplo de laço `for` e discutir como ele funciona:

```cpp
#include <iostream>

int main()
{
    for (int i{ 1 }; i <= 10; ++i)
        std::cout << i << ' ';

    std::cout << '\n';

    return 0;
}
```

Primeiro, declaramos uma variável de laço chamada `i` e a inicializamos com o valor 1.

Em segundo lugar, `i <= 10` é avaliado e, como `i` é 1, isso é avaliado como `true`. Consequentemente, a instrução é executada, que imprime `1` e um espaço.

Finalmente, `++i` é avaliado, o que incrementa `i` para 2. Então o laço volta ao segundo passo.

Agora, `i <= 10` é avaliado novamente. Como `i` tem valor 2, isso é `true`, então o laço itera novamente. A instrução imprime `2` e um espaço, e `i` é incrementado para 3. O laço continua a iterar até que eventualmente `i` seja incrementado para 11; nesse ponto, `i <= 10` é avaliado como `false` e o laço termina.

Consequentemente, este programa imprime o resultado:

```
1 2 3 4 5 6 7 8 9 10
```
### Expressões omitidas

É possível escrever laços `for` que omitem qualquer uma ou todas as instruções ou expressões. Por exemplo, no exemplo a seguir, omitiremos a instrução-inicialização e a expressão-final, deixando apenas a condição:

```cpp
#include <iostream>

int main()
{
    int i{ 0 };
    for ( ; i < 10; ) // sem instrução-inicialização ou expressão-final
    {
        std::cout << i << ' ';
        ++i;
    }

    std::cout << '\n';

    return 0;
}
```

Este laço `for` produz o resultado:

```
0 1 2 3 4 5 6 7 8 9
```

Em vez de deixar o `for` fazer a inicialização e o incremento, fizemos manualmente. Fizemos isso apenas para fins acadêmicos neste exemplo, mas há casos em que não definir uma variável de laço (porque você já tem uma) ou não incrementá-la na expressão-final (porque você está incrementando de outra forma) é desejado.

Embora não seja muito comum, vale notar que o exemplo a seguir produz um laço infinito:

```cpp
for (;;)
    instrucao;
```

O exemplo acima é equivalente a:

```cpp
while (true)
    instrucao;
```

Isso pode ser um pouco inesperado, pois você provavelmente esperaria que uma condição omitida fosse tratada como falsa. No entanto, o padrão C++ explicitamente (e inconsistentemente) define que uma condição omitida em um laço `for` deve ser tratada como verdadeira.

Recomendamos evitar completamente essa forma de `for` e usar `while (true)` em seu lugar.

### Laços for com múltiplos contadores

Embora laços `for` tipicamente iterem sobre apenas uma variável, às vezes é necessário trabalhar com múltiplas variáveis. Para ajudar nisso, o programador pode definir múltiplas variáveis na instrução-inicialização e usar o operador vírgula para alterar o valor de múltiplas variáveis na expressão-final:

```cpp
#include <iostream>

int main()
{
    for (int x{ 0 }, y{ 9 }; x < 10; ++x, --y)
        std::cout << x << ' ' << y << '\n';

    return 0;
}
```

Este laço define e inicializa duas novas variáveis: `x` e `y`. Ele itera `x` no intervalo de 0 a 9, e após cada iteração `x` é incrementado e `y` é decrementado.

## 5.10 – Break e Continue

### Break

Embora você tenha acabado de ver a instrução `break` no contexto de instruções `switch` , ela merece um tratamento mais completo, pois também pode ser usada com outros tipos de instruções de controle de fluxo. A instrução `break` faz com que um laço `while`, `do-while`, `for` ou uma instrução `switch` termine, e a execução continua com a próxima instrução após o laço ou `switch` interrompido.

#### Interrompendo um switch

No contexto de uma instrução `switch`, um `break` é tipicamente usado no final de cada `case` para indicar que o caso terminou (o que evita a cascata para casos subsequentes):

```cpp
#include <iostream>

void imprimirMatematica(int x, int y, char ch)
{
    switch (ch)
    {
    case '+':
        std::cout << x << " + " << y << " = " << x + y << '\n';
        break; // não continuar em cascata para o próximo caso
    case '-':
        std::cout << x << " - " << y << " = " << x - y << '\n';
        break; // não continuar em cascata para o próximo caso
    case '*':
        std::cout << x << " * " << y << " = " << x * y << '\n';
        break; // não continuar em cascata para o próximo caso
    case '/':
        std::cout << x << " / " << y << " = " << x / y << '\n';
        break;
    }
}

int main()
{
    imprimirMatematica(2, 3, '+');

    return 0;
}
```

#### Interrompendo um laço

No contexto de um laço, uma instrução `break` pode ser usada para encerrar o laço antecipadamente. A execução continua com a próxima instrução após o final do laço.

Por exemplo:

```cpp
#include <iostream>

int main()
{
    int soma{ 0 };

    // Permite que o usuário digite até 10 números
    for (int contador{ 0 }; contador < 10; ++contador)
    {
        std::cout << "Digite um número para somar, ou 0 para sair: ";
        int num{};
        std::cin >> num;

        // sai do laço se o usuário digitar 0
        if (num == 0)
            break; // sai do laço agora

        // caso contrário, adiciona o número à soma
        soma += num;
    }

    // a execução continuará aqui após o break
    std::cout << "A soma de todos os números digitados é: " << soma << '\n';

    return 0;
}
```

Este programa permite que o usuário digite até 10 números e exibe a soma de todos os números digitados no final. Se o usuário digitar 0, o `break` faz com que o laço termine antecipadamente (antes que 10 números sejam digitados).

Um `break` também é uma maneira comum de sair de um laço infinito intencional:

```cpp
#include <iostream>

int main()
{
    while (true) // laço infinito
    {
        std::cout << "Digite 0 para sair ou qualquer outro inteiro para continuar: ";
        int num{};
        std::cin >> num;

        // sai do laço se o usuário digitar 0
        if (num == 0)
            break;
    }

    std::cout << "Saímos!\n";

    return 0;
}
```

Um exemplo de execução:

```
Digite 0 para sair ou qualquer outro inteiro para continuar: 5
Digite 0 para sair ou qualquer outro inteiro para continuar: 3
Digite 0 para sair ou qualquer outro inteiro para continuar: 0
Saímos!
```

### Continue

A instrução `continue` fornece uma maneira conveniente de encerrar a iteração atual de um laço sem terminar o laço inteiro.

Aqui está um exemplo de uso do `continue`:

```cpp
#include <iostream>

int main()
{
    for (int contador{ 0 }; contador < 10; ++contador)
    {
        // se o número for divisível por 4, pula esta iteração
        if ((contador % 4) == 0)
            continue; // vai para a próxima iteração

        // Se o número não for divisível por 4, continua
        std::cout << contador << '\n';

        // A instrução continue salta para cá
    }

    return 0;
}
```

Este programa imprime todos os números de 0 a 9 que não são divisíveis por 4:

```
1
2
3
5
6
7
9
```

Uma instrução `continue` funciona fazendo com que o ponto atual de execução salte para o final do laço atual.

No caso de um laço `for`, a expressão-final do laço `for` (no exemplo acima, `++contador`) ainda é executada após um `continue` (já que isso acontece após o final do corpo do laço).

## Questões

# Conclusões

Parabéns! Você acaba de concluir a segunda parte do Capítulo 5 e, com ela, todo o estudo sobre controle de fluxo em C++.

Agora você tem em mãos um conjunto completo de ferramentas para controlar o fluxo dos seus programas: decisões com if e switch, repetições com while, do-while e for, e ajustes finos com break e continue. Isso é a base para construir programas verdadeiramente dinâmicos e inteligentes!

Nos vemos no próximo capítulo!

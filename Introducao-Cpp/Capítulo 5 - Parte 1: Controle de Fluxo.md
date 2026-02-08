# Capítulo 5 - Parte 1: Controle de Fluxo

## Introdução ao Controle de Fluxo

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

Para mudar isso, o C++ nos permite usar diferentes declarações de **controle de fluxo**, que nos permitem mudar o caminho normal de execução durante o programa. Já vimos um pouco disso durante o capítulo 2, introduzindo o `if` e `if-else`. Veremos agora alguns outros!

## Categorias de Instruções de Controle de Fluxo
**Categoria** | **Significado** | **Implementado em C++ por**
--- | --- | ---
Declarações condicionais | Faz com que uma sequência de código seja executada apenas se alguma condição for atendida. | `if`, `else`, `switch`
Saltos (Jumps) | Instrui a CPU a começar a executar as instruções em algum outro local. | `goto`, `break`, `continue`
Chamadas de função | Salta para outro local e retorna. | chamadas de função, `return`
Laços (Loops) | Executa repetidamente uma sequência de código zero ou mais vezes, até que uma condição seja atendida. | `while`, `do-while`, `for`, ranged-for (`for` baseado em intervalo)
Interrupções (Halts) | Termina o programa. | `std::exit()`, `std::abort()`
Exceções | Um tipo especial de estrutura de controle de fluxo projetada para tratamento de erros. | `try`, `throw`, `catch`

Conheceremos agora um pouco das instruções desta tabela!

## Declarações Condicionais

# Capítulo 1 - Parte 1: Estrutura de um Programa e Comentários

Sejam bem-vindos ao Capítulo 1 do nosso curso!

Agora que já vimos a “Hello, world!” e a instalação dos ambientes, é hora de compreender como se organiza, de fato, um programa em C++. 

Neste capítulo, daremos uma primeira olhada em alguns tópicos essenciais para qualquer programa em C++. 

Como há uma grande variedade de tópicos a serem abordados, abordaremos a maioria deles em um nível bastante superficial (apenas o suficiente para você se familiarizar). O objetivo deste capítulo é ajudar você a entender como programas básicos em C++ são construídos.

## 1.1 A Função `main`

Em C++, as instruções são normalmente agrupadas em unidades chamadas funções. Uma função é um conjunto de instruções executadas sequencialmente (em ordem, de cima para baixo).

Todo código executável deve conter uma função `main` com a seguinte assinatura:

```cpp
#include <iostream>

int main() {
    // Aqui vai o código do programa
    return 0;
}
```
Vamos analisar o exemplo "Hello, world!" do Capítulo 0:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, world!\n";
    return 0;
}
```

**Partes essenciais:**

* `#include <iostream>`: Inclui a biblioteca para entrada/saída (exibe mensagens e recebe dados do usuário).
* `int main() { ... }`: A função principal onde a execução começa. E `int` indica que a função retorna um valor inteiro.
* `std::cout`: Envia dados para a saída padrão (geralmente o terminal).
* `return 0;`: Indica que o programa terminou com sucesso.


> * Cada instrução termina com `;` (ponto e vírgula).
> * Blocos de código são delimitados por `{ }`.


## 1.2 Comentários

Um comentário é uma nota legível pelo programador, inserida diretamente no código-fonte do programa. Os comentários são ignorados pelo compilador e são para uso exclusivo do programador.

Em C++, há dois estilos diferentes de comentários, ambos com o mesmo propósito: ajudar os programadores a documentar o código de alguma forma.

### Comentários de Linha Única

O `//` símbolo inicia um comentário de linha única em C++, que instrui o compilador a ignorar tudo, desde o `//` símbolo até o final da linha. Por exemplo:

```cpp
// Comentário de uma linha
int x = 5;  // atribui 5 à variável x
```

### Comentários de Múltiplas Linhas

O par de símbolos `/*` e `*/` denota um comentário multilinha. Tudo entre os símbolos é ignorado. Por exemplo:

```cpp
/*
   Isso é um comentário
   que ocupa várias linhas.
   Útil para explicações longas!
*/
```
> Dica: use comentários para explicar **"porquês"** e não **"o quê"**. Código claro costuma dispensar comentários óbvios.

## Conclusões

Nesta primeira parte do Capítulo 1, você conheceu a estrutura básica de todo programa em C++: da inclusão de bibliotecas com #include à definição da função main.

Também vimos como inserir comentários de linha única ou múltiplas linhas para documentar o “porquê” de cada trecho, mantendo o código legível e fácil de entender.

Com esses fundamentos, você já tem as ferramentas mínimas para criar, compilar e executar programas simples, além de garantir que seus colegas (e você mesmo, no futuro) compreendam a lógica por trás de cada instrução. 

Na próxima parte falaremos de variáveis, tipos de dados e interações com o usuário, construindo em cima dessa estrutura que acabamos de estabelecer.

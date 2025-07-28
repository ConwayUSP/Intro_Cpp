# Capítulo 4 - Parte 2: Introdução à std::string

Bem vindos ao Capítulo 4, parte 2!

Neste capítulo nós falaremos um pouco mais afundo sobre o uso da **std::string** e suas características.

## 4.3 Std::string

Para trabalharmos com strings (objetos que representam uma sequência de caracteres) nós usamos `<string>` no cabeçalho do código para poder se fazer uso da std::string.

Veja o exemplo a seguir:

```cpp
#include <string>   // permite o uso de std::string

int main()
{
    std::string nome { "Coutinho" }; // inicializa o nome com a string "Coutinho"
    nome = "Little Couto";           // muda nome para "Little Couto"
    std::string meuID{ "45" };       // "45" não é o mesmo que o inteiro 45! (Não é possível manipular como número)

// Outras formas de criar e inicializar uma string
    std::string s2 = "C++";              
    std::string s3("Programming");       // Usando construtor
    std::string s4(s2);                  // Cópia de outra string
    std::string s5(5, 'a');              // String com 5 'a' characters: "aaaaa"

    return 0;
}
```

Ao usar o operador `>>` de `std::cin` para ler uma std::string, a extração interrompe-se ao encontrar o primeiro espaço em branco, tabulação ou caractere de nova linha.

Isso faz com que os nomes compostos ou frases sejam lidos apenas até a primeira palavra, deixando o restante dos caracteres no buffer de entrada.

Portanto, caso seja necessário ler uma linha completa de entrada em uma string, é melhor fazer uso da função `std::getline()` que requer dois argumentos: o primeiro é `std::cin`, e o segundo é sua variável de string. 

```cpp
#include <iostream>
#include <string> // Para std::string e std::getline

int main()
{
    std::cout << "Digite seu nome completo: ";
    std::string nome;
    std::getline(std::cin >> std::ws, nome); // lê uma linha inteira de texto em nome

    std::cout << "Digite sua entidade favorita: ";
    std::string cor;
    std::getline(std::cin >> std::ws, cor);  // lê uma linha inteira de texto em cor

    std::cout << "Seu nome é " << nome
              << " e sua entidade favorita é " << cor
              << '\n';

    return 0;
}
```
Se você quiser ignorar espaços em branco à esquerda, é necessário passar `std::cin >> std::ws` como primeiro argumento (como foi feito no código acima).

## Extras

Se quisermos saber quantos caracteres tem em uma string, podemos "perguntar" a `std::string` o seu comprimento. 

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string nome {"USPLeste"};
    std::cout << nome << " tem " << frase.length() << " caracteres\n";

    return 0;
}
```
A função `length()` retorna quantos caracteres há na string que foi passada como objeto. Esse tipo de função é chamada de função membro e, nesse caso, length() é um tipo especial de função dentro de `std::string`.

Para fazermos uso de funções membro, chamamos `objeto.função()`. 

Veja exemplos de concatenação de strings:

```cpp
#include <iostream>
#include <string>

int main() {
  std::string primeiro_nome = "Ada";
  std::string sobrenome = "Lovelace";

  // Usando o operador +
  std::string nome_completo = primeiro_nome + " " + sobrenome;

  // Usando o método .append()
  std::string saudacao = "Olá, ";
  saudacao.append(primeiro_nome);

  // Usando o operador +=
  std::string mensagem = "Bem-vindo ";
  mensagem += "ao C++!";

  std::cout << nome_completo << std::endl;
  std::cout << saudacao << std::endl;
  std::cout << mensagem << std::endl;

  return 0;
}
```

Há mais algumas funções membros que podem ser úteis no dia a dia:

- size(): retorna também o tamanho corrente da string;

- capacity(): retorna a capacidade corrente da string, ou seja, quantos elementos ela poderá conter antes de necessitar mais memória;

- max_size(): retorna o tamanho máximo possível em uma string, geralmente dependente da máquina e do compilador.

Lista com mais funções auxiliares para aprofundamento: https://www.codecademy.com/resources/docs/cpp/strings/append

## Conclusões

Nessa parte do capítulo 4 você viu o que é e como utilizar de diversas maneiras a `std::string`. Espero que tenha gostado!

Aguardo você no capítulo 5!

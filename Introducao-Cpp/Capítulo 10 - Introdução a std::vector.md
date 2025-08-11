# Capítulo 10 - Introdução a std::vector

Sejam bem-vindos ao Capítulo 10 do nosso curso!

Nesta parte do curso iremos falar sobre como trabalhar com arrays de forma dinâmica e prática através de `std::vector`. 

## 10.1 Std::vector

`std::vector` é uma classe de contêiner da biblioteca padrão do C++ (STL – Standard Template Library). Ele funciona como um array dinâmico, ou seja, pode crescer e encolher em tempo de execução conforme você insere ou remove elementos.

Declaração: 
```cpp
std::vector<Tipo> nome_do_vector;  // vetor 'nome_do_vetor' com 0 elementos do tipo 'Tipo'
```

```cpp
#include <vector>   // necessário para se utilizar std::vector
#include <string>

int main() {

  // exemplos
  std::vector<int> primos { 2, 3, 5, 7 };
  std::vector<char> vogais { 'a', 'e', 'i', 'o', 'u' };
  std::vector<int> v1(10);                 //  Vetor de 10 ints, todos inicializados com 0 (valor-padrão de int)
  std::vector<double> v2(5, 3.14);         //  Vetor de 5 doubles, todos inicializados com 3.14
  std::vector<std::string> v3(4, "ola");   //  Vetor de strings, 4 posições, cada uma com "ola"
  return 0;
}
```

Acessando e modificando elementos em um vetor:
```cpp
#include <vector>
#include <iostream>

int main() {
  std::vector<double> ordem = {3.99, 12.99, 2.49};

  // Usando o operador de índice []
  ordem[0] = 4.23;
  // Usando a função '.at()'
  ordem.at(1) = 4.23;

  // Percorre todo o vetor e imprime cada elemento
  for (double valor : ordem) {
    std::cout << valor << ' ';
  }

  // Saída: 4.23 4.23 2.49
  return 0;
}
```

Lembre-se que o primeiro elemento de um array fica no índice 0.

Adicionado elementos em um vetor:
```cpp
#include <vector>
#include <iostream>

int main() {
  std::vector<int> v = {1,2,3,4};

  // Utilizando o método ".insert()"
  v.insert(v.begin() + 1, 10);    // Insere o valor 10 na posição 1 (entre 1 e 2)
  v.insert(v.begin(), 2, 0);      // Insere 3 cópias do valor 0 no início do vetor
  
  
  // Usando o métodos para adicionar no fim do vetor
  v.push_back(5);
  v.emplace_back(6);

  for (int num : v) {
        std::cout << num << " ";
  }
  // Resultado final: [0, 0, 1, 10, 2, 3, 4, 5, 6]

  return 0;
}
```
Removendo elementos de um vetor:
```cpp
#include <vector>
#include <iostream>

int main() {
  std::vector<int> v = {1,2,3,4};

  // Usando o método "pop_back" para remover elementos
  v.pop_back();

  for (int i : v) {
    std::cout << i << " ";
  }

  return 0;
}
```
Descobrindo tamanho do vetor:
```cpp
#include <vector>
#include <iostream>

int main() {
  std::vector<int> v = {1,2,3,4};

  // Utilizando o método ".size()"
  std::cout << "Size: " << v.size();

  // Size: 4
  return 0;
}
```

## Extras

### Laço for-each

Como você deve ter notado, foi utilizado um laço `for` para percorrer todo o vetor e imprimir cada elemento em um dos exemplos dado. 

Esse tipo estrutura é chamado de laço `for-each` e possui a seguinte sintaxe:

```
for (declaração_elemento: objeto_array)
   declaração;
```

Quando um loop for baseado em intervalo é encontrado, o loop itera por cada elemento em `objeto_array`. 

Para cada iteração, o valor do elemento atual do array será atribuído à variável declarada em `declaração_elemento`, e então `declaração` será executado.

```cpp
#include <iostream>
#include <vector>

int main()
{
    std::vector <int> fibonacci { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89 };

    for (int num : fibonacci)   // itera sobre o array fibonacci and e copia cada valor em `num`
       std::cout << num << ' '; // imprime o atual valor de num`

    std::cout << '\n';

    return 0;
}
```
```
Saída: 0 1 1 2 3 5 8 13 21 34 55 89
```

### Indexação de arrays usando enums

Um dos problemas ao se trabalhar com arrays é que os  índices inteiros não fornecem nenhuma informação ao programador sobre o significado do índice. Por exemplo:

```cpp
#include <vector>

int main()
{
    std::vector notaProva { 78, 94, 66, 77, 14 };

    notaProva[2] = 76; // quem isso representa? Não está claro
}
```
Para resolver esse problema podemos usar enumeradores (enums) que permite agrupar um conjunto de valores constantes e nomeados.

```cpp
#include <vector>
#include <iostream>

namespace Estudantes {    //  organiza e agrupa identificadores pelo nome "Estudantes"
    enum Nomes {         
        Morandini,  // 0
        Digi,       // 1
        Helton,     // 2
        Violeta,    // 3
        Alexandre,  // 4
        max_estudantes // 5 (quantidade total de alunos)
    };
}

int main() {
    // Vetor de notas associado aos alunos do enum
    std::vector<int> notaProva(Estudantes::max_estudantes); // Inicializa com 5 elementos (0 a 4)

    // Atribui notas iniciais (exemplo)
    notaProva = {78, 94, 66, 77, 14};

    // Atualiza a nota de "Helton" (índice 2)
    notaProva[Estudantes::Helton] = 76;

    // Imprime todas as notas com nomes
    for (int i = 0; i < Estudantes::max_estudantes; ++i) {
        std::cout << "Aluno: " << i << ", Nota: " << notaProva[i] << "\n";
    }

    return 0;
}
```
## Questões

1) Reescreva o código abaixo usando `for-each` no lugar do for tradicional:

```cpp
std::vector<int> numeros = {4, 5, 6};
for (int i = 0; i < numeros.size(); i++) {
    std::cout << numeros[i] << " ";
}
```
2) Qual será a saída do código abaixo?
```cpp
std::vector<int> v = {1, 2, 3};
v.insert(v.begin() + 1, 99);
v.push_back(5);
v.at(0) = 10;
for (int x : v) std::cout << x << " ";
```
3) Crie um programa que:
- Use um std::vector<std::string> para armazenar itens de compras.
- Permita inserir itens no final com push_back() até o usuário digitar "fim".
- Use um for-each para exibir todos os itens.
- Mostre no final o número total de itens usando .size().

## Conclusões

Neste capítulo apresentamos o std::vector que representa arrays dinâmicos em C++, capazes de redimensionar automaticamente conforme elementos são adicionados ou removidos.

Vimos como declarar, acessar (via [] ou .at()), modificar, iterar (com for-each) e gerenciar o tamanho (com .size()).

E, por fim, vimos como usar enums para melhorar a legibilidade ao associar índices a significados claros.

Te vejo no próximo capítulo :)

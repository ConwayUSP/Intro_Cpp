# Capítulo 9: Structs e Enums

Sejam bem-vindos ao capítulo 9 do nosso curso!

Aqui, faremos uma introdução aos tipos compostos **Structs** e **Enums**. Ambos fornecem grande ajuda na estruturação de um programa robusto em **C++**, com o principal sendo o uso de **Structs**.

Sem mais delongas, vamos começar:

## 9.1 Structs

Geralmente, utilizamos as **Structs** quando estamos interessados em, por exemplo, agrupar "atributos" em específico, os quais são dizem respeito a algo em comum que estamos modelando. Esses "atributos" dizem respeito às variáveis.

Antes de qualquer coisa, precisamos definir a nossa estrutura em questão. Vamos usar um exemplo genérico de uma estrutura usada para representar algumas informações sobre uma pessoa:

**Exemplo 1: defina uma Struct Pessoa, com um espaço para nome, idade e número de registro**

Partindo de um novo arquivo **.cpp**, podemos realizar a definição da seguinte maneira:

```cpp
#include <string>

struct Pessoa{
    std::string nome;
    int idade;
    int registro;
};

int main(){

    return 0;
}
```

E, então, acabamos de definir um novo tipo a partir daquela nova estrutura. Podemos manipular ela da mesma maneira a qual fazemos com as variáveis normais: declarando novas variáveis com aquele tipo.

Para a definição de **Structs**, a convenção é sempre utilizar letras maiúsculas no primeiro caractere.

Podemos, também, interagir com cada um dos campos presente dentro do escopo. Observe:

```cpp
#include <iostream>
#include <string>


struct Pessoa{
    std::string nome;
    int idade;
    int registro;
};

int main(){

    /* Declaração da variável "fulano"
     * e "beltrano", ambos do novo tipo "Pessoa"
     */

    Pessoa fulano, beltrano;

    /* Definindo cada campo. Aqui, acessamos
     * utilizando o ponto e digitando o espaço em específico
     */

    fulano.nome = "Fulano Cacetada";
    fulano.idade = 42;
    fulano.registro = 777;

    std::cout << fulano.nome << "\n";
    std::cout << fulano.idade << "\n";
    std::cout << fulano.registro << "\n";

    std::cout << "--------------" << std::endl;

    beltrano.nome = "Beltrano Catapimbas";
    beltrano.idade = 37;
    beltrano.registro = 666;

    std::cout << beltrano.nome << "\n";
    std::cout << beltrano.idade << "\n";
    std::cout << beltrano.registro << "\n";


    return 0;
}
```

Como de costume, indicamos que você tente implementar, compilar e rodar o código.

No exemplo acima, utilizamos o acesso a cada variável constituinte da nossa nova estrutura através da sintaxe com ponto (que pode mudar para **"->"**, caso o objetivo seja desreferenciar). É possível, assim, alterar cada um daqueles espaços de maneira livre.

Uma outra maneira, mais compacta, de inicializar as variáveis também é fornecida. Acompanhe:

```cpp
#include <iostream>
#include <string>


struct Pessoa{
    std::string nome;
    int idade;
    int registro;
};

int main(){
    /* Declaração da variável "fulano"
     * e "beltrano", ambos do novo tipo "Pessoa".
     * Agora, fazemos a inicialização usando um par
     * de chaves.
     */
    Pessoa fulano {"Fulano Cacetada", 42, 777};
    Pessoa beltrano {"Beltrano Catapimbas", 3, 666};

    std::cout << fulano.nome << "\n";
    std::cout << fulano.idade << "\n";
    std::cout << fulano.registro << "\n";

    std::cout << "--------------" << std::endl;

    std::cout << beltrano.nome << "\n";
    std::cout << beltrano.idade << "\n";
    std::cout << beltrano.registro << "\n";


    return 0;
}
```

O código acima, ao ser compilado e rodado, deve produzir o mesmo resultado observado anteriormente a partir do outro programa.

Para mais detalhes acerca da inicialização das variáveis de uma estrutura, não deixe de conferir o [Capítulo 13.8](https://www.learncpp.com/cpp-tutorial/struct-aggregate-initialization/) do [Learn C++](https://www.learncpp.com/).

As estruturas também podem ser utilizadas como argumentos e retornos de funções.

**Exemplo 2: faça uma função chamada novaPessoa, que retorne o tipo Pessoa. Ela deve criar uma variável daquele tipo(que será retornado) e pedir para que o usuário insira o nome, a idade e o número de registro dela**

Aqui, não existe nenhum segredo. Após a definição da estrutura, podemos considerá-la como apenas mais uma variável no nosso arsenal.

O código da nossa função pode ser estruturado da seguinte maneira:

```cpp
Pessoa novaPessoa(){
    Pessoa nova;

    std::cout << "Insira o nome da pessoa: ";
    std::getline(std::cin >> std::ws, nova.nome); //Aqui, utilizamos uma funcionalidade da #include <string>

    std::cout << "Insira a idade da pessoa: ";
    std::cin >> nova.idade;

    std::cout << "Insira o número do registro da pessoa: ";
    std::cin >> nova.registro;

    return nova;
}
```

**Exemplo 3: faça uma função void chamada imprimePessoa. Ela deve receber como argumento uma estrutura do tipo Pessoa e imprimir cada um de seus atributos**

Aqui, também, não existe algo fora de nossa capacidade. Podemos elaborar essa função da seguinte forma:

```cpp
void imprimePessoa(Pessoa pessoa){

    std::cout << "Imprimindo informações:" << std::endl;
    std::cout << "-----------------------" << std::endl;
    std::cout << "Nome: "<< pessoa.nome << "\n";
    std::cout << "Idade: "<< pessoa.idade << "\n";
    std::cout << "Registro: "<< pessoa.registro << "\n";
}
```

Ou seja, ao passar como parâmetro, aqui temos livre acesso às variáveis constituintes.

Agora, e quando trabalhamos com ponteiros?

Com as **Structs**, somos capazes, inclusive, de fazer algo do tipo:

```cpp
struct Pessoa{
    std::string nome;
    int idade;
    int registro;
    Pessoa * prox;
};
```

No caso, dentro do próprio escopo da estrutura, podemos declarar uma variável com o tipo dela.

Como mencionado anteriormente, utilizamos, ao invés do ponto, a sintaxe **->** para [desreferência implícita do objeto ponteiro antes de selecionar o membro](https://www.learncpp.com/cpp-tutorial/member-selection-with-pointers-and-references/).

Isto é, Pessoa->idade é, por exemplo, equivalente a (*Pessoa).idade

A partir disso, vamos para mais um exemplo:

**Exemplo 4: considere a nova versão apresentada acima da estrutura Pessoa. Crie três pessoas a partir da função novaPessoa, depois faça com que as três estejam conectadas umas com as outras a partir do novo campo Pessoa * prox. Por fim, imprima o conteúdo das três, usufruindo do novo campo e da função imprimePessoa. Faça todas as alterações necessárias nas funções anteriormente implementadas**

Aqui, já não temos um ponto tão trivial quanto os anteriores. Vamos precisar reescrever as funções anteriormente implementadas com base nas novas informações recebidas.

Como vamos conectar as três pessoas através do ponteiro agora presente na estrutura **Pessoa**, precisaremos declará-las, também, como objetos ponteiros.

Um passo de cada vez. Vamos começar pelas alterações em **novaPessoa**.

Agora, ela deverá retornar um ponteiro para **Pessoa**. Desse modo, precisaremos alterar a declaração realizada na função, para ponteiro para Pessoa, e os acessos normais a cada um de seus campos, para a sintaxe de desreferência implícita.

Observe:

```cpp
Pessoa * novaPessoa(){

    //Aqui, colocamos também o alocamento necessário
    Pessoa * nova = new Pessoa;

    //Daqui em diante, todos os campos são acessados com "->"
    std::cout << "Insira o nome da pessoa: ";
    std::getline(std::cin >> std::ws, nova->nome);

    std::cout << "Insira a idade da pessoa: ";
    std::cin >> nova->idade;

    std::cout << "Insira o número do registro da pessoa: ";
    std::cin >> nova->registro;

    //Boa prática:
    nova->prox = nullptr;

    std::cout << "\n";

    return nova;
}
```

Caso você já tenha alguma base em C, o "new Pessoa" é equivalente aqui ao "(Pessoa *)malloc(sizeof(Pessoa))". Bem mais amigável, não?

Vamos tratar, então, da função **imprimePessoa**.

No caso, precisamos alterar o argumento para um **ponteiro para Pessoa** e, simplesmente, alterar os acessos. Vamos lá:

```cpp
void imprimePessoa(Pessoa * pessoa){

    std::cout << "Imprimindo informações:" << std::endl;
    std::cout << "-----------------------" << std::endl;
    std::cout << "Nome: "<< pessoa->nome << "\n";
    std::cout << "Idade: "<< pessoa->idade << "\n";
    std::cout << "Registro: "<< pessoa->registro << "\n" << "\n";
}
```

Em seguida, na função main, podemos estruturar nossas ideias da seguinte maneira:

```cpp
int main(){

    //Estruturando nossas três pessoas
    Pessoa * pessoa1 = novaPessoa();
    Pessoa * pessoa2 = novaPessoa();
    Pessoa * pessoa3 = novaPessoa();

    //Conectando elas através do espaço prox
    pessoa1->prox = pessoa2;
    pessoa2->prox = pessoa3;

    //Loop para chamar a imprimePessoa, iterando pelas pessoas conectadas
    for(Pessoa * temp = pessoa1; temp; temp = temp->prox) imprimePessoa(temp);

    //Liberando memória alocada
    delete pessoa1;
    delete pessoa2;
    delete pessoa3;

    return 0;
}
```

E se quisermos utilizar múltiplos arquivos e headers?

**Exemplo 5: divida o projeto em três arquivos: main.cpp, myFunctions.cpp, myFunctions.h. Ele deve permanecer funcionando da mesma maneira**

Caso você já tenha lido o capítulo 3, apenas siga sua intuição. Acompanhe a resolução:

```
main.cpp
```
```cpp
#include <iostream>
#include <string>
#include "myFunctions.h"

int main(){

    Pessoa * pessoa1 = novaPessoa();
    Pessoa * pessoa2 = novaPessoa();
    Pessoa * pessoa3 = novaPessoa();

    pessoa1->prox = pessoa2;
    pessoa2->prox = pessoa3;

    for(Pessoa * temp = pessoa1; temp; temp = temp->prox) imprimePessoa(temp);

    delete pessoa1;
    delete pessoa2;
    delete pessoa3;

    return 0;
}
```

```
myFunctions.cpp
```
```cpp
#include <iostream>
#include <string>
#include "myFunctions.h"


Pessoa * novaPessoa(){

    Pessoa * nova = new Pessoa;

    std::cout << "Insira o nome da pessoa: ";
    std::getline(std::cin >> std::ws, nova->nome);

    std::cout << "Insira a idade da pessoa: ";
    std::cin >> nova->idade;

    std::cout << "Insira o número do registro da pessoa: ";
    std::cin >> nova->registro;

    nova->prox = nullptr;

    std::cout << "\n";

    return nova;
}

void imprimePessoa(Pessoa * pessoa){

    std::cout << "Imprimindo informações:" << std::endl;
    std::cout << "-----------------------" << std::endl;
    std::cout << "Nome: "<< pessoa->nome << "\n";
    std::cout << "Idade: "<< pessoa->idade << "\n";
    std::cout << "Registro: "<< pessoa->registro << "\n" << "\n";
}
```

```
myFunctions.h
```
```cpp
#include <iostream>
#include <string>

struct Pessoa{
    std::string nome;
    int idade;
    int registro;
    Pessoa * prox;
};

Pessoa * novaPessoa();
void imprimePessoa(Pessoa * pessoa);
```

Por fim, vamos falar um pouco de **Templates** com **Structs**.

O conceito anteriormente apresentado neste curso também se aplica às estruturas. Vamos retornar a um exemplo de função do **Capítulo 7**:

```cpp
// Template de função para encontrar o máximo entre dois valores
template <typename T> // Declaração do template (T é um tipo genérico)
T maximo(T a, T b) {
    return (a > b) ? a : b;
}
```

A ideia é a mesma para as estruturas.

**Exemplo 6: faça uma Struct chamada de Par. Dentro de seu escopo, ela deve ter duas variáveis. Utilize tipos genéricos**

Intuitivamente, conseguimos chegar no resultado. Olhe:

```cpp
template <typename I>
struct Par{
    I primeiro;
    I segundo;
};
```

A partir daqui, podemos manipular a estrutura com base em tipos genéricos. Nomeamos isso como **Class templates**.

Aqui, um exemplo de aplicação utilizando ambos acima:

```cpp
#include <iostream>

// Declaração do template (T é um tipo genérico)
template <typename T>
// Template de função para encontrar o máximo entre dois valores
T maximo(T a, T b) {
    return (a > b) ? a : b;
}

template <typename I>
struct Par{
    I primeiro;
    I segundo;
};

int main(){

    Par<int> p1{7, 3};
    Par<double> p2{2.1, 6.9};

    std::cout << "O máximo entre 7 e 3 é: " << maximo(p1.primeiro, p1.segundo) << "\n";
    std::cout << "O máximo entre 2.1 e 6.9 é: " << maximo(p2.primeiro, p2.segundo) << "\n";


    return 0;
}
```

Para mais detalhes aprofundados, recomendamos os capítulos [13.13](https://www.learncpp.com/cpp-tutorial/class-templates/) e [13.14](https://www.learncpp.com/cpp-tutorial/class-template-argument-deduction-ctad-and-deduction-guides/) do [Learn C++](https://www.learncpp.com/).

## Conclusões

Nesta primeira parte do Capítulo 9, você teve um vislumbre de como funcionam as **Structs** em C++.

A linguagem é muito rica em detalhes e oferece muitas utilidades. A consulta às nossas principais referências é sempre recomendada caso você queira ter uma noção mais completa acerca de todos os pontos.

Na próxima parte, falaremos de **Enums**. Não deixe de acompanhar!

Até a próxima parte!

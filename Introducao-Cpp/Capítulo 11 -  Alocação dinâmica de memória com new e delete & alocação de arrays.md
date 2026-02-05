# Capítulo 11 - Alocação dinâmica de memória com new e delete & alocação de arrays

Sejam bem-vindos ao Capítulo 11 do nosso curso!

Nesta parte do curso iremos falar sobre alocação dinâmica e suas propriedades.

## 11.1 Alocação dinâmica

Pense em um cenário onde podemos querer usar uma string para armazenar o nome de alguém, mas não sabemos o comprimento do nome até que a pessoa o digite. Ou podemos estar criando um jogo com um número variável de monstros (que muda ao longo do tempo à medida que alguns monstros morrem e outros surgem) tentando matar o jogador.

Nesses tipos de situações, uma possível solução seria estimar e alocar o tamanho máximo das variáveis ​​de que precisaremos e torcer para que seja suficiente.

Entretanto, essa seria uma solução inadequada, uma vez que isso levaria ao desperdício de memória se as variáveis ​​não forem realmente usadas. Por exemplo, se alocarmos 25 caracteres para cada nome, mas os nomes em média têm apenas 12 caracteres, estaremos usando mais que o dobro do que realmente precisamos.

Então, para resolver esses tipos de problemas nós utilizamos a **alocação dinâmica de memória**:

`Processo de reservar espaço na memória RAM (especificamente na área heap) durante a execução do programa (runtime), e não na compilação. Ela permite gerenciar o tamanho da memória sob demanda usando os operadores new (alocar) e delete (liberar), sendo essencial para estruturas de dados cujo tamanho é desconhecido antecipadamente.`

## 11.2 Operadores "new" e "delete"

O `new` faz um pedido ao sistema operacional: "Reserve um espaço deste tamanho e me diga onde ele está". Ele retorna o **endereço de memória** desse espaço, que deve ser armazenado em um ponteiro.

O `delete` não apaga o ponteiro em si, mas sim **libera a memória** que o ponteiro está apontando. Ele informa ao sistema operacional que aquele bloco de memória na Heap está disponível para ser usado por outros programas ou outras partes do seu código.
 
```cpp
#include <iostream>

int main() {
    // 1. CUIDADO: Isso aloca memória, mas como o endereço não é salvo, 
    // ela se torna inacessível. Criamos um "Memory Leak" (vazamento).
    new int; 

    // 2. ALOCAÇÃO CORRETA: O endereço retornado pelo new é salvo no ponteiro 'ptr'.
    int* ptr{ new int }; 

    // 3. USO: Acessamos esse espaço na Heap desreferenciando o ponteiro.
    *ptr = 7; 

    std::cout << "Valor na Heap: " << *ptr << std::endl;

    // 4. LIBERAÇÃO: Devolvemos a memória ao sistema.
    delete ptr; 
    ptr = nullptr; // Boa prática: evita que o ponteiro aponte para memória liberada.

    return 0;
}
```
Uma regra importante é que para cada `new` no seu código, deve haver um `delete` correspondente para que o sistema operacional recupere o espaço.

Note que após usar `delete ptr;`, o ponteiro `ptr` ainda guarda o endereço antigo, mas a memória lá já não pertence mais a você. Por isso, definimos `ptr = nullptr;` logo em seguida, para evitar que tentemos acessar aquele endereço por erro.

## 11.3 Alocação dinâmica de arrays

Além de alocar valores individuais dinamicamente, também podemos alocar arrays de variáveis ​​dinamicamente. 

Ao contrário de um array fixo, cujo tamanho deve ser definido em tempo de compilação, a alocação dinâmica de um array permite escolher seu comprimento em tempo de execução (ou seja, o comprimento não precisa ser uma constante de tempo em compilação).

Para alocar um array dinamicamente, usamos a forma de array de new e delete (frequentemente chamadas de `new[]` e `delete[]`):

Veja um exemplo abaixo:

```cpp
#include <iostream>

int main() {
    // 1. Pergunta o tamanho ao usuário
    std::cout << "Digite o tamanho do array: ";
    int tamanho;
    std::cin >> tamanho;

    // 2. ALOCAÇÃO: Cria um array na Heap com o tamanho escolhido.
    // O '{}' no final inicializa todos os elementos com zero.
    int* array = new int[tamanho]{}; 

    std::cout << "Array de tamanho " << tamanho << " criado na Heap.\n";

    // 3. USO: Atribui o valor 5 ao primeiro elemento (índice 0)
    array[0] = 5; 

    // 4. LIBERAÇÃO: Como usamos 'new[]' para um array, 
    // precisamos usar 'delete[]' para devolver a memória.
    delete[] array; 

    // Nota: Aqui não precisamos fazer 'array = nullptr' porque o programa 
    // termina logo em seguida e a variável 'array' deixará de existir.

    return 0;
}
```
## Questões

1) Escreva um programa que peça ao usuário um número real (double). Aloque esse número dinamicamente usando `new`, peça para o usuário digitar o valor, exiba o dobro desse valor e, por fim, desaloque a memória corretamente. Não esqueça de anular o ponteiro no final.

2) Crie um programa que pergunte ao usuário quantas notas ele deseja registrar.
- Aloque um array dinamicamente com esse tamanho.
- Use um laço for para preencher as notas.
- Calcule a média aritmética das notas.
- Exiba a média e libere a memória do array.

3) Caça ao erro

Analise o trecho de código abaixo e identifique dois erros graves de gerenciamento de memória. Explique por que estão errados e como corrigi-los:

```cpp
void criarDados() {
    int* ptr = new int[10];
    ptr[0] = 50;
    
    if (ptr[0] > 0) {
        return; 
    }

    delete ptr;
}
```

## Conclusões

Neste capítulo apresentamos o conceito de alocação dinâmica e vimos que os operadores `new` e `delete` permitem alocar variáveis ​​individuais dinamicamente para nossos programas.

A memória alocada dinamicamente tem duração dinâmica e permanecerá alocada até que você a desaloque ou o programa termine.

Você também viu que o uso de `new[]` e `delete[]` permite que o programa se adapte à demanda de dados em tempo real, alocando arrays com tamanhos definidos apenas durante a execução.

Te vejo no curso de POO :)

# Capítulo 0 - Parte 2: Hello, world!

Olá! Sejam bem vindos à segunda parte do Capítulo 0 do nosso curso!

Neste capítulo, abordaremos o famoso ritual de passagem para o início de aprendizado em
qualquer linguagem de programação: "Hello, world!".

Escreveremos, então, esse código na sintaxe do C++ e abordaremos mais alguns detalhes.

**Lembrando: utilizaremos, por padrão, o GCC (GNU Compiler Collection) para compilar nossos
códigos neste curso.**

Sem mais delongas, vamos começar!

## Criando o arquivo

O primeiro passo é **criar um arquivo com extensão .cpp**, como, por exemplo, **Hello.cpp**.

Caso sua IDE forneça algum processo "automatizado" de criação de arquivo com a extensão específica do C++ (.cpp), então fique à vontade para utilizar.

Entretanto, aqui traremos um exemplo de maneira livre, para que nosso curso seja o mais abrangente possível.

No Linux, caso você não saiba, podemos fazer digitando um comando da seguinte maneira ao abrir o terminal
no local aonde você deseja salvar o arquivo:

```
touch Hello.cpp
```

Depois disso, abra o arquivo, ou o diretório onde ele se encontra, utilizando sua IDE e, então, vamos
começar a codificar!

## Escrevendo o código

Começaremos, então, incluindo a **iostream**, que é uma abreviação para **"standard input-output stream"**.
Ela é a biblioteca mais genérica do C++, análoga à stdio.h da linguagem C.

À grosso modo, uma biblioteca é um "arsenal" de códigos/funcionalidades da linguagem. Para utilizar
esses recursos, precisamos incluí-la no nosso código. Assim, vamos escrever na primeira linha:

```C++
#include <iostream>
```

ou...

```C++
#include "iostream"
```


Nitidamente, a inclusão de bibliotecas segue a sintaxe a qual utilizamos nos dois casos acima. Ambos funcionam. **"#include"** para incluir e, dentro de um par de aspas duplas ou de parênteses angulares, o
nome da biblioteca a qual você quer.

Em breve, nos capítulos posteriores, comentaremos mais um pouco sobre a **iostream**.

Em seguida, vamos criar a nossa função principal, que, por padrão, terá de ser a **main** (intuitivo, não?).

Então, nas próximas linhas, escreveremos:

```C++
int main(){

}
```

Este será o corpo da nossa **função main**. Futuramente, abordaremos mais profundamente o uso de funções
no nosso código. No momento, apenas entenda que uma função em programação é algo bem análogo às funções
da matemática: recebem valores como parâmetros/argumentos dentro do par de parênteses e, funcionando como
uma "máquina", ela te retorna um valor após fazer as alterações necessárias no sistema.

É aonde iremos "guardar" o nosso algoritmo escrito em código para utilizá-lo depois apenas "chamando"
ela em outra parte do código geral. E, por padrão, tudo gira em torno da função main: é o coração do
nosso programa.

Prosseguindo, vamos digitar dentro das chaves da nossa função o seguinte:

```C++
std::cout <<
```

Que serve para mostrar uma imagem na tela. E, após os dois parênteses angulares, escreveremos
nossa mensagem dentro de um par de aspas duplas:

```C++
std::cout << "Hello, world!\n";
```

O contrabarra seguido por n representa **a quebra de linha**. Ou seja, pularemos para a próxima linha
do terminal após imprimirmos a mensagem. Ah, sim: não esqueça do bendito **;** após sua linha de algoritmo.

Após isso, nosso código estará assim:

```C++
#include <iostream>

int main() {
    std::cout << "Hello, world!\n";
}
```

Perceba que, antes do nome da nossa função, colocamos **int**, que representa o tipo de dados os quais
serão retornados pela função. No caso, ela retornará um valor inteiro. Nos próximos capítulos, falaremos
mais sobre os tipos de dados.
Precisamos, então, definir um valor a ser retornado. Nesse caso, podemos colocá-la para retornar, por exemplo, **o valor 0**, que é o padrão para a função main.

Então, faremos nosso último passo e escreveremos o seguinte após o código de impressão:

```C++
#include <iostream>

int main() {
    std::cout << "Hello, world!\n";
    return 0;
}
```

O "return 0" serve, justamente, para que a função retorne o valor zero após executar o seu passo a passo o qual escrevemos.
Ufa! Por fim, temos nosso primeiro código em C++. Não esqueça de salvá-lo.

## Compilando o código usando GCC

Agora que já temos nosso arquivo com o código necessário para o "Hello, world!", precisamos apenas
compilá-lo para que vire um arquivo executável e realize sua programação.

Para compilá-lo usando o GCC, podemos fazer da seguinte maneira:

Abra seu terminal no local onde o arquivo .cpp se encontra e faça o seguinte comando:

```
g++ Hello.cpp -o Hello
```

Ou...

```
g++ -o Hello Hello.cpp
```

No caso, utilizamos **"g++"** para "chamar" o compilador. E, depois, escrevemos **-o** e, em seguida, o nome que queremos para o arquivo de saída junto com o nome do arquivo .cpp (antes ou depois, no caso).

Assim, basta apertar enter e, caso não tenha feito nada de errado, você terá um novo arquivo, executável, **no mesmo lugar o qual está seu .cpp**.

Por fim, basta executar o arquivo

```
./Hello
```
(Exemplo no terminal Linux)

e você receberá no terminal a seguinte mensagem:

```
Hello, world!
```

E, parabéns! Você escreveu seu primeiro código em C++.

## Conclusões

Neste capítulo, você passou pelo ritual mais básico do aprendizado de uma linguagem: o "Hello, world!".

A partir daqui, exploraremos juntos esse vasto mundo da programação em C++.

Vejo você nos próximos capítulos! :)

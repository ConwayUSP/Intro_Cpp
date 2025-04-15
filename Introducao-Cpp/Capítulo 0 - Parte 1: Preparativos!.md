# Capítulo 0 - Parte 1: Preparativos!

Sejam bem vindos ao Capítulo 0 do nosso curso!

Antes de mais nada, temos como objetivo apresentar alguns exemplos de ambientes de programação (IDEs)
apropriados para o desenvolvimento utilizando a nossa querida linguagem C++.

Além disso, é claro, como estamos tratando de uma linguagem compilada, apresentaremos os principais
compiladores voltados para ela.

Por fim, na segunda parte, teremos a condificação do clássico "Hello World" e alguns detalhes envolvidos.

Sem mais delongas. Vamos iniciar:

## **IDEs recomendadas**

Quando falamos de IDE, o que não falta é opção! Existe uma quantidade enorme de softwares editores
de texto que podem ser bem interessantes, cada um com suas vantagens e desvantagens.

Vale ressaltar que, neste curso, não iremos nos apoiar numa IDE específica, isto é, se você
tiver coragem, mesmo, e estiver com vontade de codificar utilizando o bloco de notas, será
plenamente possível.

Então, iniciando:

### Dev-C++

Começando, então, com um dos clássicos: o Dev-C++.

Ele pode aparentar ser uma IDE feia, que passa a impressão de ser razoavelmente datada.
Porém, ela tem o povo!
Para uma pessoa a qual está iniciando com seus primeiros passos no mundo da programação
com windows, especialmente utilizando C/C++, o Dev-C++ é a primeira referência.
De acordo com o site oficial do software:

**"is a full-featured C and C++ Integrated Development Environment (IDE) for Windows platforms. Millions of developers, students and researchers use Dev-C++ since the first version was released in 1998. It has been featured in dozens of C++ and scientific books and remains one of the favorite learning tool among universities & schools worldwide."**

**"é um Ambiente de Desenvolvimento Integrado (IDE) completo em C e C++ para plataformas Windows. Milhões de desenvolvedores, estudantes e pesquisadores utilizam o Dev-C++ desde o lançamento da primeira versão em 1998. Ele já foi mencionado em dezenas de livros científicos e de C++ e continua sendo uma das ferramentas de aprendizado favoritas entre universidades e escolas do mundo todo."**

Site oficial para download (é gratuito!): https://www.bloodshed.net/

### Visual Studio Code (VSCode)

Este aqui é dos mais famosos (se não, o mais famoso) entre os desenvolvedores mundo à fora.

Claro, não poderia faltar a menção ao VSCode. É uma das maiores ferramentas para o Desenvolvimento
de software. Muito poderosa, cheia de pacotes e extensões. Além, é claro, de utilizar um terminal
linux e programação em nuvem, com integração ao GitHub, o que é muito útil de modo geral.

Porém, um dos contras é que, dependendo do tamanho do projeto ou da quantidade de adições feitas
na estrutura do software, ele pode perder BASTANTE desempenho, ainda mais se você estiver utilizando
o famoso laptop da Xuxa. Existem opções que também são poderosas e não perdem desempenho dessa maneira.
É válido ressaltar que estaremos trabalhando com desempenho em nossas implementações para computação
gráfica, então alta peformance é sempre bem vinda.

Um ponto positivo, também, é que ele é acessível tanto para windows, macOS, quanto para uma quantidade
boa de distribuições linux. Ou seja, ele é mais acessível do que, por exemplo, o Dev-C++.

Site oficial para download (é gratuito!): https://code.visualstudio.com/

### Sublime Text

Este é uma opção bem decente e leve para edição de texto.

O Sublime é, com certeza, uma ferramenta muito poderosa, mesmo em sua versão gratuita.

Ele possui, também, muitas extensões e pacotes para compor a sua programação, sem perda de
desempenho como ocorre no VSCode. Ele é acessível, também, para múltiplos sistemas operacionais
e não exige uma curva de aprendizado grande para aprender. Seus macros, também, são um diferencial
bem bacana.

Um exemplo de desvantagem é que ele não possui, pelo menos em sua versão gratuita, um integração direta com
nuvem (arquivos locais), nem um terminal integrado. Ou seja, a não ser que você encontre uma extensão que inclua de
maneira decente um terminal no software, é necessário compilar externamente, com algum terminal instalado em sua máquina.
Porém, esses detalhes podem ser contornados, se necessário, utilizando os pacotes. Basta pesquisar um pouco e ver
a disponibilidade. É claro, caso você saiba utilizar seu terminal, nem será necessário buscar essas adições e
o Sublime, possivelmente, será uma escolha maravilhosa para ti.

Site oficial para download (tem a versão gratuita e paga): https://www.sublimetext.com/

### Zed

Aqui, estamos falando do famoso (ou nem tanto) "VSCode killer".

Atualmente, quando estamos escrevendo este capítulo, ele ainda é muito recente e não atingiu sua versão 1.0.

Porém, mesmo assim, ele é uma escolha muito interessante, pois mistura a leveza do Sublime com as ferramentas
do VSCode. Inclusive, ele é capaz de utilizar os macros de diferentes IDEs e possui suporte para muitas linguagens.

Atualmente, ele não inclui vínculo direto com o GitHub, mas já possui suporte nativo para Git. Além disso, possui
um terminal bem rápido integrado no seu design. Estamos falando de uma IDE extremamente flexível e com bastante
potencial para o futuro, além de, novamente, ser bem leve.

Um ponto negativo é que, por enquanto, ele não possui suporte para Windows, somente para macOS e distros Linux.
Porém, fortemente recomendamos este aqui caso seja acessível para você. E, dependendo de quando você está lendo
isto, ele pode já ter sido expandido para o sistema da Microsoft.

Site oficial para download (é gratuito!): https://zed.dev/

## **Escolhendo um compilador**

Escolher um compilador é pré-requisito essencial para programar na linguagem C++, afinal é ele que traduz o código
escrito nela para linguagem de máquina.

### GCC (GNU Compiler Collection)

Uma das principais referências para compilar código em C/C++ é, justamente, o GCC.

Nem temos muito o que falar sobre este aqui. É, simplesmente, clássico e multiplataforma (funciona em Windows,
Linux e MacOS).

Inclusive, será o principal compilador o qual utilizaremos para este curso. Esta, então, é nossa principal
recomendação.

Link para download: https://gcc.gnu.org/
(Inclusive, caso você esteja utilizando alguma distribuição Linux específica, tal como Ubuntu,
saiba que o GCC já vem instalado por padrão, então não precisa baixar novamente. Para garantir,
você pode pesquisar para ver se seu compilador está atualizado).

### Clang

Como uma outra opção para compilar, nós temos o Clang, que pode ser uma opção útil caso você
não queira utilizar o GCC, por qualquer motivo que seja.

Link do Site do compilador: https://clang.llvm.org/

## Conclusões

Nesta primeira parte da aula zero, apenas sugerimos algumas ferramentas que serão essenciais nesta
trajetória.

Obviamente, caso você sinta maior conforto utilizando alguma IDE ou algum compilador os quais não foram
aqui citados, sinta-se à vontade. Além disso, sobre os compiladores, utilizar algum nativo de alguma IDE,
como aquele presente, por exemplo, no VSCode, é sempre uma opção (contanto que isso não limite o seu aprendizado!).

Prosseguiremos, na próxima parte deste capítulo, com o famoso "Hello World" e alguns detalhes referentes à
estruturação desse código.

Obrigado por ter chegado até aqui e até a próxima parte!

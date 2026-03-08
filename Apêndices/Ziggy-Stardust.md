# Apêndice 00 - Compilando código C++ com Zig! (Ou Ziggy-Stardust)

Sejam bem vindos ao primeiro apêndice do nosso curso!

Aqui, neste diretório, você encontrará markdowns com informações variáveis que possam ser úteis para o desenvolvimento em C++.

Começaremos utilizando o compilador Zig para compilar nossos programas em C++.

> 🎵 🎶 Now Ziggy played guitar

> Jamming good with Weird and Gilly

> And The Spiders from Mars

> He played it left hand

> But made it too far

> Became the special man

> Then we were Ziggy's band 🎵 🎶

## O que diabos é Zig?

Zig é uma linguagem de programação de alto nível (ou baixo? depende do que você interpreta neste ponto em específico), compilada e com tipagem estática. 

De acordo com a própria documentação, Zig é projetada para ser mais eficiente e fácil de usar do que as linguagens existentes.

De acordo com o [site oficial](https://ziglang.org/), em tradução livre,

> Zig é uma linguagem de programação e um conjunto de ferramentas de propósito geral para a manutenção de software robusto, otimizado e reutilizável.

Apesar de ser uma linguagem recente (pobre _betinha_), Zig já tem uma comunidade ativa e uma vasta biblioteca de pacotes disponíveis. Ela possui muito potencial para o desenvolvimento de software moderno, rivalizando até mesmo com as linguagens mais antigas e um dos queridinhos da atualidade: [Rust](https://www.rust-lang.org/)! (Inclusive, temos uma trilha que aborda essa linguagem -> [Lucky Crab](https://github.com/ConwayUSP/Lucky_Crab))

## Como usar Zig para compilar C++?

Algo curioso é que essa linguagem dialoga com o compilador C++ nativo do sistema operacional, permitindo a compilação de código C++ diretamente. O mesmo vale para a linguagem C.

Geralmente, utilizamos MakeFiles para automatizar a compilação de programas em C++. Com Zig, isso é simplificado e mais eficiente. Por isso, decidimos escrever esse apêndice para mostrar como fazer isso. Você não precisa aprender Zig de maneira aprofundada para usar essa funcionalidade (apesar de ser bem interessante e super válido caso você tenha tempo para isso). Apenas, siga a nossa querida receita de bolo!

## Como instalar Zig?

Instalar o Zig é um processo bastante direto, pois o compilador é distribuído como um binário único autossuficiente. Você não precisa lidar com instaladores complexos ou dependências pesadas de sistema. 

Vamos lá:

### 1. Usando gerenciadores de pacotes

Esta é a maneira mais fácil de manter o Zig atualizado. Caso você tenha o Windows (saia dessa vida, faça um favor a si mesmo(a)), você pode rodar o seguinte comando no PowerShell para utilizar winget ou scoop:

```sh
winget install zig.zig
# OU
scoop install zig
```

Para macOS, 

```
brew install zig
```

Por último, mas não menos importante, para Linux: embora existam nos repositórios oficiais (sudo apt install zig), eles costumam estar bem desatualizados. O ideal é usar o Snap para garantir a versão mais recente. Observe:

```sh
sudo snap install zig --classic --beta
```

Após instalar, é só abrir um novo terminal e digitar:

```sh
zig version
```

Isso deve exibir a versão do Zig instalada. Se você vir algo como `command not found`, tente reiniciar o terminal.

## Receita de bolo

### O comando básico

Para compilar um arquivo C++ simples, você substitui o tradicional g++ ou clang++ por zig c++:

```sh
zig c++ main.cpp -o programa
```

### Compilando com bibliotecas

Para incluir bibliotecas externas, você pode usar o `-I` para especificar diretórios de cabeçalhos e `-L` para especificar diretórios de bibliotecas:

```sh
zig c++ main.cpp -o programa -I /caminho/para/cabecalhos -L /caminho/para/bibliotecas
```

### Compilando com flags

Você pode passar flags adicionais para o compilador usando `-f`:

```sh
zig c++ main.cpp -o programa -f
```

### Compilação Cruzada

Para compilar para uma plataforma diferente da sua, use o `-target`. Por exemplo, se você está no Linux e quer gerar um executável para Windows (.exe):

```sh
zig c++ main.cpp -o programa -target x86_64-pc-linux-gnu
```

No caso, cada plataforma tem sua própria sintaxe para o '-target'. Segue, então, uma tabelinha para você consultar sempre que necessário:

| Sistema Operacional | Arquitetura | Target do Zig |
| :--- | :--- | :--- |
| **Windows** | 64-bit | x86_64-windows-gnu |
| **Linux** | 64-bit | x86_64-linux-gnu |
| **macOS (Intel))** | 64-bit | x86_64-macos-none |
| **macOS (M1/M2)** | ARM | aarch64-macos-none |

### A cereja do bolo: usando o build.zig para projetos maiores

Se o seu projeto tem vários arquivos e dependências, em vez de scripts bash complexos ou Makefiles, você pode usar o sistema de build do próprio Zig.

Crie um arquivo chamado build.zig na raiz e utilize o seguinte código como exemplo:

```zig
const std = @import("std");

pub fn build(b: *std.Build) void {
    const target = b.standardTargetOptions(.{});
    const optimize = b.standardOptimizeOption(.{});

    const exe = b.addExecutable(.{
        .name = "meu_projeto",
        .target = target,
        .optimize = optimize,
    });

    // Adiciona os arquivos C++
    exe.addCSourceFile(.{ .file = .{ .path = "src/main.cpp" }, .flags = &[_][]const u8{"-std=c++17"} });
    
    // Linka com a biblioteca padrão do C++
    exe.linkLibCpp();

    b.installArtifact(exe);
}
```

Ficou assustado(a) com o tamanho do código? Não se preocupe, o build.zig é extremamente flexível e pode ser personalizado conforme suas necessidades.

De qualquer maneira, vamos desmembrar o exemplo acima para que você não se sinta totalmente no escuro.

O código começa com a importação do módulo `std` do Zig. É semelhante a `#include <stdio.h>` em C, ou `#include <iostream>` em C++.

Em seguida, definimos uma função `build` que recebe um ponteiro para um objeto `std.Build`. Dentro dessa função, configuramos o target e as opções de otimização padrão do projeto. Além disso, acionamos o método addExecutable para adicionar um executável ao projeto. Depois, adicionamos os arquivos C++ ao executável usando o método addCSourceFile. Por fim, linkamos com a biblioteca padrão do C++ usando o método linkLibCpp e instalamos o executável usando o método installArtifact.

Para compilar, use o comando:

```sh
zig build
```

Você obterá um executável instalado em `zig-out/bin/`.

O zig c++ pode ser ligeiramente mais lento que o Clang nativo na primeira execução porque ele precisa "preparar" as bibliotecas padrão para o target escolhido, mas o cache subsequente é muito eficiente.

## Conclusões

Neste exemplo, aprendemos como usar o build.zig para compilar um projeto C++ simples. O zig c++ é uma ferramenta poderosa e flexível que pode ser usada para construir projetos de qualquer tamanho e complexidade. Ter uma ferramenta como essa no seu arsenal é extremamente útil quando se trabalha com C++.

Novamente, caso queira mergulhar na linguagem Zig, o próprio site possui uma [documentação completa](https://ziglang.org/documentation/) e uma [comunidade ativa](https://ziglang.org/community/).

Por enquanto, é isso. Até mais!

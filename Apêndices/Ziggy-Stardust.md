# Apêndice 00 - Compilando código C++ com Zig! (Ou Ziggy-Stardust)

Sejam bem vindos ao primeiro apêndice do nosso curso!

Aqui, neste diretório, você encontrará markdowns com informações variáveis que possam ser úteis para o desenvolvimento em C++.

Começaremos utilizando o compilador Zig para compilar nossos programas em C++.

> 🎵 🎶 Now Ziggy played guitar 🎵 🎶

> 🎵 🎶 Jamming good with Weird and Gilly 🎵 🎶

> 🎵 🎶 And The Spiders from Mars 🎵 🎶

> 🎵 🎶 He played it left hand 🎵 🎶

> 🎵 🎶 But made it too far 🎵 🎶

> 🎵 🎶 Became the special man 🎵 🎶

> 🎵 🎶 Then we were Ziggy's band 🎵 🎶

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
zig c++ main.cpp -o programa -target x86_64-windows-gnu
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

> ⚠️ Atenção: Mudanças na API do Zig
Como o Zig está em desenvolvimento contínuo (em direção à versão 1.0), sua API de compilação sofre atualizações. Os exemplos abaixo utilizam a sintaxe mais recente e recomendada das versões modernas (0.14.0+), que utilizam Módulos Raiz (root_module) e a função b.path() para gerenciar caminhos de forma segura.

Crie um arquivo chamado build.zig na raiz e utilize o seguinte código como exemplo:

```zig
const std = @import("std");

pub fn build(b: *std.Build) void {
    const target = b.standardTargetOptions(.{});
    const optimize = b.standardOptimizeOption(.{});

    // 1. Cria o executável e define seu Módulo Raiz
    const exe = b.addExecutable(.{
        .name = "meu_projeto",
        .root_module = b.createModule(.{
            .target = target,
            .optimize = optimize,
        }),
    });

    // 2. Adiciona os arquivos C++
    exe.root_module.addCSourceFile(.{ 
        .file = b.path("src/main.cpp"), 
        .flags = &[_][]const u8{"-std=c++17"} 
    });
    
    // 3. Linka com a biblioteca padrão do C++
    exe.linkLibCpp();

    // 4. Instala o executável
    b.installArtifact(exe);
}
```

Ficou assustado(a) com o tamanho do código? Não se preocupe, o build.zig é extremamente flexível e pode ser personalizado conforme suas necessidades.

De qualquer maneira, vamos desmembrar o exemplo acima para que você não se sinta totalmente no escuro.

O código começa com a importação do módulo `std` do Zig. É semelhante a `#include <stdio.h>` em C, ou `#include <iostream>` em C++.

Em seguida, definimos uma função build que recebe um ponteiro para um objeto std.Build. Dentro dessa função, configuramos o target e as opções de otimização padrão do projeto. Além disso, acionamos o método addExecutable para adicionar um executável ao projeto, passando para ele um root_module que concentra as configurações. Depois, adicionamos os arquivos C++ ao módulo do executável usando o método addCSourceFile e a função b.path(). Por fim, linkamos com a biblioteca padrão do C++ usando o método linkLibCpp e instalamos o executável usando o método installArtifact.

E se eu quiser compilar múltiplos arquivos? 

Para compilar múltiplos arquivos com o sistema de build do Zig, você tem dois caminhos "principais", dependendo de quão organizado (ou preguiçoso) você quer ser.

#### 1. Lista Manual (addCSourceFiles)

Esta é a forma mais comum. Em vez de chamar a função para cada arquivo, você passa um array de strings. É ideal para quando você quer ter controle total sobre o que entra. Em vez de addCSourceFile (singular), use addCSourceFiles (plural).

Olhe o exemplo abaixo:

```zig
const cpp_files = [_][]const u8{
    "src/main.cpp",
    "src/engine.cpp",
    "src/physics/collision.cpp",
    "src/utils/logger.cpp",
};

exe.addCSourceFiles(.{
    .files = &cpp_files,
    .flags = &[_][]const u8{ "-std=c++17", "-Wall" },
});
```

No caso, criamos um array com os caminhos dos arquivos e passamos para addCSourceFiles.

#### 2. Usando uma Pasta Raiz (root)

Se todos os seus arquivos estão dentro de uma pasta src, você pode definir um root para não precisar repetir o caminho em cada string. O Zig resolverá os caminhos relativos a essa pasta.

```zig
exe.root_module.addCSourceFiles(.{
    .root = b.path("src"), // Pasta raiz onde estão os arquivos
    .files = &[_][]const u8{
        "main.cpp",
        "renderer.cpp",
        "input.cpp",
    },
    .flags = &[_][]const u8{"-std=c++20"},
});
```

No caso, definimos `src` como root e os caminhos são relativos a ele.

#### 3. Lidando com Arquivos de Cabeçalho

Por fim, para lidar com arquivos de cabeçalho (.hpp / .h), é necessário adicionar o caminho da pasta onde eles estão. Suponha que você tenha uma pasta "include" que contenha essa parte do seu projeto. Veja:

```zig
exe.root_module.addIncludePath(b.path("include"));
```

O que o código acima faz é adicionar o caminho "include" à lista de caminhos de inclusão do executável, permitindo que os arquivos `.hpp` e `.h` sejam encontrados corretamente.

Simples assim!

#### 4. Exemplo completo

Vamos supor que você está fazendo um jogo e precisa compilar vários arquivos fonte. Veja um exemplo completo:

```zig
const std = @import("std");

pub fn build(b: *std.Build) void {
    const target = b.standardTargetOptions(.{});
    const optimize = b.standardOptimizeOption(.{});

    const exe = b.addExecutable(.{
        .name = "meu_jogo",
        .root_module = b.createModule(.{
            .target = target,
            .optimize = optimize,
        }),
    });

    // 1. Onde estão os seus arquivos .hpp ou .h
    exe.root_module.addIncludePath(b.path("include"));

    // 2. Adicionando os arquivos fonte
    exe.root_module.addCSourceFiles(.{
        .root = b.path("src"),
        .files = &[_][]const u8{
            "main.cpp",
            "game.cpp",
            "graphics.cpp",
        },
        .flags = &[_][]const u8{ "-std=c++17", "-O3" },
    });

    // 3. OBRIGATÓRIO para C++
    exe.linkLibCpp();

    b.installArtifact(exe);
    
    // Bônus: Comando para executar o programa diretamente
    const run_cmd = b.addRunArtifact(exe);
    run_cmd.step.dependOn(b.getInstallStep());
    const run_step = b.step("run", "Executa o jogo");
    run_step.dependOn(&run_cmd.step);
}
```

O código acima combina a adição de caminhos de inclusão, arquivos fonte e bibliotecas C++ em um único executável. É um combo dos pontos que tocamos anteriormente. Um bom exercício para você é explicar mentalmente como cada linha do código contribui para a compilação final.

Para compilar, use o comando:

```sh
zig build
```

Para compilar e já executar o projeto automaticamente, use o comando:

```sh
zig build run
```

Você obterá um executável instalado em `zig-out/bin/`.

O zig c++ pode ser ligeiramente mais lento que o Clang nativo na primeira execução porque ele precisa "preparar" as bibliotecas padrão para o target escolhido, mas o cache subsequente é muito eficiente.

## Exercício

Construa a seguinte estrutura de diretórios para o seu projeto:

```
projeto_ziggy/
├── build.zig
├── include/
│   └── space_utils.hpp
└── src/
    ├── main.cpp
    └── space_utils.cpp
```

No cabeçalho, faça a declaração da seguinte função:

```cpp
void tocarGuitarra();
```

Em seguida, implemente a função no arquivo `space_utils.cpp`:

```cpp
#include "space_utils.hpp"

void tocarGuitarra() {
    std::cout << "Ziggy played guitar, jamming good with Weird and Gilly!" << std::endl;
}
```

Por fim, chame a função no arquivo `main.cpp`:

```cpp
#include "space_utils.hpp"

int main() {
    tocarGuitarra();
    return 0;
}
```

O desafio é construir a build.zig para compilar o projeto! Revise o que for necessário e use sua intuição!

## Conclusões

Neste exemplo, aprendemos como usar o build.zig para compilar um projeto C++ simples. O zig c++ é uma ferramenta poderosa e flexível que pode ser usada para construir projetos de qualquer tamanho e complexidade. Ter uma ferramenta como essa no seu arsenal é extremamente útil quando se trabalha com C++.

Novamente, caso queira mergulhar na linguagem Zig, o próprio site possui uma [documentação completa](https://ziglang.org/documentation/) e uma [comunidade ativa](https://ziglang.org/community/).

Por enquanto, é isso. Até mais!

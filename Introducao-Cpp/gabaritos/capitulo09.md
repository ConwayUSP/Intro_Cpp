# Capítulo 09

## Parte 1: Structs

### Exercício 1: Modelagem de produto

```cpp
#include <iostream>
#include <string>

struct Produto {
    std::string nome;
    double preco;
    int estoque;
};

void exibirProduto(Produto p) {
    std::cout << "Produto: " << p.nome << " | R$ " << p.preco 
              << " | Estoque: " << p.estoque << std::endl;
}

int main() {
    // Inicialização por ponto
    Produto p1;
    p1.nome = "Teclado";
    p1.preco = 150.0;
    p1.estoque = 10;

    // Inicialização por chaves
    Produto p2 {"Mouse", 80.0, 20};

    exibirProduto(p1);
    exibirProduto(p2);

    return 0;
}
```

### Exercício 2: Playlist

```cpp
#include <iostream>
#include <string>

struct Musica {
    std::string titulo;
    Musica* proxima;
};

int main() {
    // Alocação dinâmica
    Musica* m1 = new Musica{"The Art of Dying", nullptr};
    Musica* m2 = new Musica{"Silvera", nullptr};

    // Conectando com o operador seta ->
    m1->proxima = m2;

    // Percorrendo a lista
    for (Musica* atual = m1; atual != nullptr; atual = atual->proxima) {
        std::cout << "Tocando: " << atual->titulo << std::endl;
    }

    delete m1;
    delete m2;
    return 0;
}
```

### Exercício 3: Coordenadas Genéricas (Struct Templates)

```cpp
#include <iostream>

// 1. Definindo o template da estrutura para aceitar tipos variados (int, double, etc)
template <typename T>
struct Ponto {
    T x;
    T y;
};

// 2. Função template para imprimir as coordenadas de qualquer tipo de Ponto
template <typename T>
void imprimirPonto(Ponto<T> p) {
    std::cout << "Coordenadas: (" << p.x << ", " << p.y << ")" << std::endl;
}

int main() {
    // 3. Instanciando Ponto com inteiros (pixels de tela)
    Ponto<int> tela {1920, 1080};
    
    // 4. Instanciando Ponto com doubles (coordenadas GPS)
    Ponto<double> gps {-23.5505, -46.6333};

    std::cout << "Ponto da Tela: ";
    imprimirPonto(tela);

    std::cout << "Ponto GPS: ";
    imprimirPonto(gps);

    return 0;
}
```


## Parte 2: Enums

### Exercício 1: Status de pedido

```cpp
#include <iostream>

enum StatusPedido {
    Pendente,
    Processando,
    Enviado,
    Entregue
};

void imprimirStatus(StatusPedido status) {
    switch(status) {
        case Pendente:    std::cout << "Pedido Pendente"; break;
        case Processando: std::cout << "Pedido em Processamento"; break;
        case Enviado:     std::cout << "Pedido Enviado"; break;
        case Entregue:    std::cout << "Pedido Entregue"; break;
    }
    std::cout << std::endl;
}

int main() {
    StatusPedido meuPedido = Pendente;
    imprimirStatus(meuPedido);
    return 0;
}
```

### Exercício 2: Conversão de Tipos (Clima)

```cpp
#include <iostream>

enum Clima {
    Desconhecido = 0,
    Ensolarado,
    Chuvoso
};

int main() {
    // Inicialização segura com valor zero (Desconhecido)
    Clima hoje{}; 

    if (hoje == Desconhecido) {
        std::cout << "Alerta: Clima nao definido!" << std::endl;
    }

    // Atribuindo valor via cast
    hoje = static_cast<Clima>(1); // Ensolarado
    std::cout << "Valor atual do clima: " << hoje << std::endl;

    return 0;
}
```

### Exercício 3: Sistema de Clima

```cpp
#include <iostream>

// 1. Definindo a enumeração com o valor zero como "Desconhecido"
enum Clima {
    Desconhecido = 0, // Boa prática: reserva o 0 para estado padrão
    Ensolarado,       // 1
    Chuvoso,          // 2
    Nevando           // 3
};

int main() {
    // 2. Inicialização por chaves inicializa a enum com o valor zero (Desconhecido)
    Clima hoje{}; 

    // 3. Verificação do estado padrão
    if (hoje == Desconhecido) {
        std::cout << "Alerta: Clima nao definido no sistema!" << std::endl;
    }

    // 4. Alterando o valor para um estado válido
    hoje = Ensolarado;

    if (hoje != Desconhecido) {
        std::cout << "O clima atual e conhecido. Valor: " << hoje << std::endl;
    }

    return 0;
}
```

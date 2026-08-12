[README.md](https://github.com/user-attachments/files/30966004/README.md)
# 🎨 Gothic Paint

Um programa de desenho estilo "Paint" feito em **C++** com **SFML 3**, com uma interface escura (gothic) e layout vertical, pensado para uso em modo retrato (900x1600).

Conta com pincel, borracha, formas geométricas, paleta de cores, undo/redo e exportação em PNG — tudo isso em um único arquivo, sem dependências externas além da própria SFML.

---

## ✨ Funcionalidades

- **Pincel** e **Borracha** com tamanho ajustável
- Ferramentas de forma: **Linha**, **Retângulo** e **Círculo**
- **Paleta de cores** fixa com 16 tons (clique para trocar a cor atual)
- **Desfazer / Refazer** (histórico de até 30 estados)
- **Limpar tela**
- **Salvar** o desenho como `gothic_paint.png`
- Renderização em `sf::RenderTexture`, separando o canvas do restante da interface (barra superior, barra lateral e barra de status)

---

## ⌨️ Controles

| Tecla         | Ação                  |
|---------------|-----------------------|
| `B`           | Pincel                |
| `E`           | Borracha              |
| `L`           | Linha                 |
| `R`           | Retângulo             |
| `C`           | Círculo                |
| `+`           | Aumentar tamanho do pincel |
| `-`           | Diminuir tamanho do pincel |
| `Ctrl + Z`    | Desfazer              |
| `Ctrl + Y`    | Refazer               |
| `Ctrl + S`    | Salvar imagem (PNG)   |
| `Delete`      | Limpar o canvas       |
| Clique na paleta | Trocar cor atual   |

---

## 🧱 Estrutura do projeto

```
gothic paint          # código-fonte principal (C++)
```

A lógica está toda encapsulada na classe `GothicPaint`, responsável por:

- **Loop principal** (`executar`) — eventos, atualização e desenho
- **Entrada** (`processarEventos`, `processarMouse`, `processarTeclado`) — captura de mouse e teclado
- **Desenho no canvas** (`desenharPincel`, `desenharLinha`, `desenharRetangulo`, `desenharCirculo`)
- **Histórico** (`salvarEstado`, `desfazer`, `refazer`)
- **Interface** (`desenharTopo`, `desenharBarraLateral`, `desenharPaleta`, `desenharStatus`)

---

## 🔧 Requisitos

- Compilador com suporte a **C++17** (ou superior)
- [SFML 3.x](https://www.sfml-dev.org/) (o código usa a API nova, com `sf::VideoMode({W, H})`, `event->getIf<...>()`, etc. — **não é compatível com SFML 2.x**)

### Instalando a SFML

**Linux (Debian/Ubuntu):**
```bash
sudo apt install libsfml-dev
```

**macOS (Homebrew):**
```bash
brew install sfml
```

**Windows:** baixe os binários em [sfml-dev.org/download](https://www.sfml-dev.org/download.php) ou use o [vcpkg](https://github.com/microsoft/vcpkg):
```bash
vcpkg install sfml
```

---

## ▶️ Como compilar e executar

> O arquivo-fonte não tem extensão `.cpp` no repositório. Renomeie/copie antes de compilar:

```bash
cp "gothic paint" gothic_paint.cpp
```

**Compilando manualmente com g++:**
```bash
g++ -std=c++17 gothic_paint.cpp -o gothic_paint \
    -lsfml-graphics -lsfml-window -lsfml-system

./gothic_paint
```

**Com CMake** (exemplo de `CMakeLists.txt`):
```cmake
cmake_minimum_required(VERSION 3.16)
project(GothicPaint LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(SFML 3 COMPONENTS Graphics Window System REQUIRED)

add_executable(gothic_paint gothic_paint.cpp)
target_link_libraries(gothic_paint PRIVATE SFML::Graphics SFML::Window SFML::System)
```

```bash
mkdir build && cd build
cmake ..
cmake --build .
./gothic_paint
```

---

## 🖼️ Salvando desenhos

Pressione `Ctrl + S` a qualquer momento. A imagem é salva no diretório de execução como `gothic_paint.png`.

---

## 🚧 Possíveis melhorias futuras

- Ferramenta de preenchimento (`Fill`) — já existe no `enum Tool`, mas ainda não está implementada
- Zoom e seleção de área (há um espaço reservado em `atualizar()`)
- Seletor de cor customizada (RGB/hex), além da paleta fixa
- Botões da barra lateral funcionais (atualmente são apenas visuais)
- Suporte a redimensionamento de janela

---

## 📄 Licença

Projeto pessoal de estudo. Sinta-se livre para usar como referência.

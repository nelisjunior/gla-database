# Páginas e Funcionalidades

## Home — `index.html`

### Abas: Memory e Quiz

- **Memory**: grade de 12 quadrados (4x3). Cada quadrado abre um seletor de “cores” (imagens) e a cor escolhida vira o background do quadrado.
- **Quiz**:
  - Campo de texto filtra uma lista grande de frases.
  - Filtro ignora acentos (normalização NFD) e faz `includes`.
  - Cada frase tem um `type` (`true`/`false`) que vira classe CSS.

### Módulos (containers) acessados por botões

- **Planejador de Diamantes**: abre `dima.html`.
- **Mapa Interativo**: abre `map.html`.
- **Planejador de Coliseu**: abre `coliseum.html`.
- **Receitas**: abre um container interno (sem trocar de página).
- **Baús e Conquistas**: abre um container interno.
- **World Boss Ranking**: abre um container interno.

Observação: há botões comentados para `rotation.html` e `tracklist.html`.

## Receitas — dentro da Home

- Lista `foods` com requisitos (nível), cooldown (segundos) e ingredientes.
- Permite multiplicar a receita por um valor (1 a 100) e calcula:
  - Quantidade total de cada ingrediente
  - Custo total (somando `ingredients.cost`)

## Baús e Conquistas — dentro da Home

### Baús

- Menu lateral lista todas as `islands`.
- A lista de baús mostra:
  - ID do baú
  - Itens do baú (imagem + quantidade quando >1)
  - Aviso (`chest.w`) quando existe
- Clique no baú abre um mapa (overlay) com:
  - Zoom/pan
  - Troca de andar (up/down)
  - Centralização no baú clicado
  - Coordenadas em % no hover

### Conquistas

- Lista de `achievements` com nome e descrição.
- Ao clicar, exibe detalhes (nome + descrição). Há um array `directions`, mas atualmente a Home cria `<img>` sem setar `src`.

## World Boss Ranking — dentro da Home

- Mostra lista de bosses (`worldBosses`) e ranking por data.
- Regra de UI:
  - Se boss selecionado é **Marineford**, exibe coluna `Tempo`.
  - Caso contrário, esconde `Tempo` e renomeia o cabeçalho para `Dano`.

## Mapa Interativo — `map.html`

- Seletor de ilha (modal grid) com imagem + nome.
- Mapa com zoom/pan e troca de andar.
- Renderiza:
  - **Baús** (`islands[].chests`) com numeração
  - **Ovos** (`islands[].eggs`) com numeração e opcional `warn`
- Permite marcar/desmarcar (X) baús e ovos com clique.
- Persistência das marcações via `localStorage`.

## Rotations — `rotation.html`

- Mostra rotações atuais (`rotationOne`, `rotationTwo`, `specialRot`) e lista completa de personagens (`chars`).
- Filtros:
  - Por texto (nome)
  - Por classes (AND)
  - Por “idade” da rotação (cores)

## Planejador de Diamantes — `dima.html`

- Seleção de personagens soma contadores por “tags” (classes).
- Permite filtrar por texto e por classes.

## Criador de Grupo (TeamBuilder) — `teambuilder.html`

- Slots do grupo:
  - Tank
  - 4x DPS (aceita personagens `DPS` **ou** `Bruiser`)
  - Support
- Ao selecionar um slot, a lista é filtrada para personagens válidos.

## Planejador de Coliseu — `coliseum.html`

- Interface com ligas/slots (inimigos fixos) e seleção de personagens para cada slot.
- Compartilhamento:
  - Encode de seleção em `?chars=...` (string com IDs de 2 caracteres)
  - Botão “Criar Link” copia para a área de transferência.
- Evita duplicidade: ao escolher um personagem que já estava em outro slot, ele é removido do slot anterior.

## To Do List — `tracklist.html`

- Controle de tarefas semanais/evento por conta.
- Persiste em `localStorage` (`accounts`).
- Tem layout desktop e mobile (seleção de conta por setas no mobile).

## Glaguessr — `glaguessr.html`

- Navegador de ilhas que abre mapas por andar e mostra coordenadas em % no hover.
- Não possui persistência.

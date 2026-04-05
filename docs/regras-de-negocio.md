# Regras de Negócio (extraídas do código)

Este documento descreve regras observáveis no comportamento do app. Onde aplicável, a regra é citada com o “por quê” (como o código faz).

## Navegação e visibilidade (Home)

- Containers internos (Receitas, Baús/Conquistas, World Boss) são **mutuamente exclusivos**: abrir um fecha os outros.
- `#memory` e `#quiz` controlam qual aba aparece na Home.

## Memory (Home)

- Existem **12 quadrados** (`numberOfSquares = 12`).
- Cada quadrado pode receber uma entre as 6 cores (`colors = [blue, purple, pink, orange, green, red]`).
- **Reset** (e tecla Espaço) coloca todos os quadrados como `black`.

## Quiz (Home)

- O filtro:
  - é **case-insensitive**;
  - ignora **acentos**;
  - faz busca por **substrings** (`includes`).
- As frases possuem `type` (`true`/`false`) aplicado como classe CSS no item renderizado.

## Receitas (Home)

- Quantidade (`multiplier`):
  - entrada é “sanitizada” para aceitar apenas números;
  - mínimo 1;
  - botões definem: 1, -1, +1, 100.
- Custo total:

$$\text{custoTotal} = \sum_{ingrediente} (custoUnit\_{ingrediente} \times qtd\_{ingrediente} \times multiplier)$$

- Cada ingrediente mostrado depende de correspondência exata entre `foods[].ing` e `ingredients[].name`.

## World Boss (Home)

- Seleção de boss reseta `selectedWbDate = 0`.
- Exibição condicional:
  - **Marineford**: exibe coluna `Tempo` e o cabeçalho fica `Wave`.
  - Outros bosses: esconde `Tempo` e o cabeçalho vira `Dano`.
- Navegação por datas:
  - botões esquerda/direita respeitam o tamanho do array `worldBosses[].dates`.

## Baús (Home)

- Os itens do baú são renderizados buscando dados em `items`.
- Quantidade maior que 1 mostra etiqueta com `formatToK`:
  - `<1000`: mostra número
  - `>=1000`: mostra em `k` (ex.: `1500` -> `1.5k`)
- Se existir `chest.w`, o baú exibe um indicador de aviso.

## Mapa do Baú (Home)

- Coordenadas são exibidas em porcentagem (0..100) no hover.
- O mapa abre centralizado no baú clicado com zoom-alvo `2.5` (limitado pelo `maxZoom` da Home, que é 1; isso impede zoom acima de 1 na implementação atual).

## Conquistas (Home)

- Lista de conquistas (`achievements`) é exibida com nome/descrição.
- Ao selecionar uma conquista, o painel de detalhes mostra nome/descrição.
- O array `directions` existe, mas a UI atual não atribui `src` aos `<img>` criados.

## Mapa Interativo (map.html)

- Renderiza **baús** e **ovos** por ilha e por andar.
- Marcação (toggle):
  - Clique em um ícone marca/desmarca e adiciona um `X`.
  - Persistência via `localStorage` usando chaves:
    - `markedChests`
    - `markedEggs`
  - O ID salvo é derivado de `island.name`, tipo (chest/egg), índice e andar.
- `egg.warn` (ex.: `+1`, `-2`) indica deslocamento de andar quando alguns andares estão faltando.

## Rotations (rotation.html)

- `lastDate` é a referência para classificar a “idade” da última rotação:
  - `< 1 semana`: `green` (atual)
  - `< 4 semanas`: `white` (até 1 mês)
  - `< 8 semanas`: `orange` (até 2 meses)
  - `>= 8 semanas`: `red` (mais de 2 meses)
- Se o personagem contém a tag `noRot`, ele aparece como “fora das rotações”.
- Filtro por classes é do tipo **AND**: o personagem precisa conter **todas** as classes selecionadas.

## Planejador de Diamantes (dima.html)

- Seleção de personagem:
  - clicar alterna selecionado/não-selecionado;
  - ao selecionar, incrementa **um contador para cada tag** que o personagem possui e que exista no mapeamento de botões (`dimaButtons`).
- Filtros:
  - texto por substring
  - classes via conjunto ativo (`activeFilters`) com lógica AND

## TeamBuilder (teambuilder.html)

- Ao selecionar um slot, ativa filtros de classe para mostrar apenas personagens compatíveis.
- Slots DPS aceitam personagens com classe `DPS` **ou** `Bruiser`.
- Reset do grupo apenas troca as imagens para `None`.

## Coliseum (coliseum.html)

- Cada seleção é serializada em URL:
  - 2 caracteres por slot (`chars[].id`)
  - query param `?chars=...`
- Regra de unicidade:
  - se um personagem for escolhido e já estiver em outro slot, ele é removido do slot anterior.
- O botão “Criar Link” copia o link gerado via Clipboard API.

## To Do List (tracklist.html)

- `name` (conta) deve ser único; duplicatas disparam alerta.
- Campos e limites:
  - `wanted`: 0..30, incremento/decremento de 2
  - `boss`: 0..11, incremento/decremento de 1
  - `prove`: 0..8, incremento/decremento de 1
- Reordenação:
  - botões movem a conta para cima/baixo no array
  - exclusão remove a conta
- Evento:
  - range configurado em `eventOn.start` e `eventOn.end`
  - dias fora do range ficam desabilitados no calendário
  - navegação de meses é limitada ao mês inicial e final do evento

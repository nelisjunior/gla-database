# Dados e Modelos

Este documento descreve **o formato dos dados** usados pelas páginas.

## `constants.js`

### `chars` (Rotations)

Formato:

- `name`: string
- `type`: string (ex.: `dima`, `gold`)
- `dates`: string[] no formato `DD-MM-YYYY` (ordem: mais recente primeiro)
- `image`: caminho da imagem
- `class`: string[] (tags/classes; pode conter `noRot`)

Observações:

- `lastDate` (string `DD-MM-YYYY`) é a referência para o cálculo de “cor/idade” da última rotação.
- `rotationOne`, `rotationTwo` e `specialRot` são derivados de `chars` via `getRotationChars(...)`.

### `foods` e `ingredients` (Receitas)

`foods`:

- `name`: string
- `img`: string
- `lvl`: number
- `cd`: number (segundos)
- `ing`: Array<object> onde cada objeto mapeia `nomeDoIngrediente -> quantidade`

`ingredients`:

- `name`: string (deve bater com as chaves usadas em `foods[].ing`)
- `cost`: number (custo unitário em berries)
- `img`: string

### `worldBosses` (Ranking)

Formato:

- `name`: string
- `img`: string
- `dates`: array
  - `date`: string (ex.: `27/09/2024` ou `A ser adicionado`)
  - `ranking`: array
    - `rank`: number
    - `players`: string[] (6 nomes)
    - `wave`: number (semântica varia por boss; na Home vira `Wave` ou `Dano`)
    - `time`: string (apenas exibido para Marineford na Home)

### `items` (Catálogo de itens)

- `name`: string
- `img`: string

Esse catálogo é usado para renderizar as imagens dos itens listados em `islands[].chests[].items`.

### `islands` (Mapas, baús e ovos)

`islands[]`:

- `name`: string
- `maps`: string[] (um caminho por andar; o índice do array é o número do andar)
- `chests`: array
  - `id`: number (ID exibido)
  - `items`: array
    - `item`: string (deve existir em `items[].name`)
    - `quantity`: number
  - `floor`: number
  - `x`: number (0..100 em %)
  - `y`: number (0..100 em %)
  - `w` (opcional): string (aviso mostrado na Home)
- `eggs` (opcional): array
  - `id`: number
  - `floor`: number
  - `x`: number (0..100)
  - `y`: number (0..100)
  - `warn` (opcional): string (ex.: `+1`, `-2`)

### `achievements`

- `name`: string
- `description`: string
- `img`: string
- `directions`: string[] (atualmente não é usado plenamente na Home)

### `updateText`

String exibida no painel de “news” na Home.

## Dados fora de `constants.js`

Algumas ferramentas possuem datasets próprios:

- `dima.js`: array `chars` reduzido, com `name`, `image`, `class`
- `teambuilder.js`: array `chars` com classes, incluindo versões timeskip
- `coliseum.js`: array `chars` com `id` de 2 caracteres para serialização em URL
- `tracklist.js`: o “modelo” de conta é persistido em `localStorage`

### Modelo de conta (`tracklist.js`)

Cada conta persistida em `localStorage.accounts` segue (na criação):

- `name`: string
- `raid`: boolean
- `wanted`: number (0..30, passo 2)
- `boss`: number (0..11)
- `prove`: number (0..8)
- `global`: boolean[5] (Quiz, Count, Race, Memory, Deathmatch)
- `coliseum`: boolean[2] (Coliseum, One Man Army)
- `event`: { `days`: boolean[N] } (N depende do range do evento configurado)

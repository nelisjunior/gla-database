# Guia de Atualização de Dados

Este guia foca nas áreas em que o projeto funciona como “banco de dados” (principalmente `constants.js`).

## Atualizar texto de novidades (Home)

- Editar `updateText` em `constants.js`.

## Atualizar receitas

### Adicionar/editar comida (`foods`)

Em `constants.js`:

- Garanta `name`, `img`, `lvl`, `cd`.
- Em `ing`, as chaves devem ser nomes de ingredientes existentes em `ingredients[].name`.

### Adicionar/editar ingrediente (`ingredients`)

- `name` precisa ser único.
- `cost` deve ser numérico (berries).
- `img` deve existir em `Img/Food/Ingredientes/`.

## Atualizar World Boss

Em `constants.js` -> `worldBosses`:

- Cada boss tem `dates[]`.
- Cada `date` contém `ranking[]`.
- O campo `wave` é usado como:
  - **Wave** para Marineford
  - **Dano** para outros bosses (apenas muda o rótulo na UI)

## Atualizar catálogo de itens (`items`)

- Ao adicionar itens novos usados em baús, inclua também no array `items` para que a Home consiga renderizar imagem.

## Atualizar ilhas/mapas/baús/ovos (`islands`)

### Mapas

- `maps` é um array: cada entrada é o caminho do PNG de um andar.
- A numeração de andares usada pelo app é o índice do array (`0..maps.length-1`).

### Baús (`islands[].chests[]`)

- `floor` deve ser um andar válido.
- `x` e `y` são percentuais (0..100) relativos à imagem do andar.
- `items[]`:
  - `item` deve existir em `items[].name`.
  - `quantity` deve ser número.
- `w` (opcional) é um texto de aviso (ex.: “só uma vez por conta”).

### Ovos (`islands[].eggs[]`)

- Mesmo esquema de `floor`, `x`, `y`.
- `warn` (opcional): string como `+1`, `-2`.

## Atualizar conquistas (`achievements`)

- Cada item tem `name`, `description`, `img`, `directions`.
- Observação: na UI atual da Home, `directions` não atribui `src` automaticamente.

## Atualizar rotações (`chars`)

- As datas em `chars[].dates` precisam estar no formato `DD-MM-YYYY`.
- Atualize `lastDate` quando quiser alterar a referência da “rotação atual” para o cálculo de cores.
- `rotationOne/Two/specialRot` são definidos no próprio arquivo a partir de nomes.

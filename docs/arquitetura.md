# Arquitetura

## Stack

- **Frontend**: HTML/CSS/JavaScript puro (sem build)
- **Assets**: imagens em `Img/`, áudios em `Audio/`
- **Fonte/Ícones**: Google Fonts (Roboto) e Material Symbols (via CDN)

## Organização

- Cada ferramenta é uma página independente:
  - `index.html` + `index.js` + `index.css`
  - `map.html` + `map.js` + `map.css`
  - `rotation.html` + `rotation.js` + `rotation.css`
  - `dima.html` + `dima.js` + `dima.css`
  - `teambuilder.html` + `teambuilder.js` + `teambuilder.css`
  - `coliseum.html` + `coliseum.js` + `coliseum.css`
  - `tracklist.html` + `tracklist.js` + `tracklist.css`
  - `glaguessr.html` + `glaguessr.js` + `glaguessr.css`

## “Banco de dados” em `constants.js`

As páginas abaixo dependem de `constants.js`:

- Home (`index.html`)
- Mapa Interativo (`map.html`)
- Rotations (`rotation.html`)
- Glaguessr (`glaguessr.html`)

`constants.js` expõe (entre outros):

- `chars` (rotações)
- `foods` e `ingredients` (receitas)
- `worldBosses` (ranking)
- `items`, `islands` (baús/mapas/ovos)
- `achievements` (conquistas)
- `updateText` (texto de novidades exibido na Home)

## Design tokens

O projeto usa variáveis CSS (ex.: `--background`, `--border`, `--foreground`). Elas aparecem repetidas em múltiplos CSS e funcionam como um “mini design system”.

## Estado e navegação

- Home: alterna abas via `window.location.hash` e `history.pushState`.
- Ferramentas: navegação por `window.location.replace('index.html')` no botão de voltar.
- Persistência local:
  - `map.js`: marcações de baús/ovos (toggle com clique, salva em `localStorage`).
  - `tracklist.js`: lista de contas e checklists.

## Segurança e privacidade (escopo do projeto)

- O app não faz chamadas a servidor e não envia dados.
- Dados persistidos ficam **apenas no navegador** via `localStorage`.
- A única integração com o navegador além de UI é:
  - `navigator.clipboard.writeText(...)` no Planejador de Coliseu.

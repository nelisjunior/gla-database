# Operação e Deploy

## Rodar localmente

Como é um projeto estático, existem duas opções:

1) Abrir `index.html` diretamente no navegador.
2) Servir com um servidor estático (recomendado). No VS Code, o projeto já tem configuração para Live Server:

- `.vscode/settings.json`: `liveServer.settings.port = 5501`

## Publicar

Pode ser publicado em qualquer host estático (GitHub Pages, Netlify, Vercel (modo estático), Cloudflare Pages etc.).

Requisitos:

- Preservar a estrutura de pastas (principalmente `Img/` e `Audio/`).
- Atenção a **case-sensitive paths** em ambientes Linux (ex.: `Img/Maps` vs `Img/maps`).

## Compatibilidade

- Depende de recursos modernos:
  - `URLSearchParams`
  - `localStorage`
  - Clipboard API (`navigator.clipboard.writeText`)

## Persistência

Limpar dados:

- Para resetar o Mapa Interativo, limpe `localStorage` das chaves `markedChests` e `markedEggs`.
- Para resetar o To Do List, limpe `localStorage.accounts` (ou use o botão Resetar dentro da página).

# Visão Geral

## O que é

O **GLA Database** é um conjunto de páginas estáticas (Vanilla **HTML/CSS/JavaScript**) que funcionam como uma “base de conhecimento” e um conjunto de ferramentas para o jogo **GLA** (ex.: receitas, baús, ranking de World Boss, planejadores).

Não existe backend, build, bundler ou dependências via npm: o projeto roda diretamente no navegador e pode ser publicado em qualquer hospedagem estática.

## Público-alvo

- Jogadores que querem consultar dados (baús, conquistas, receitas, ranking) e usar planejadores.
- Mantenedores que atualizam os dados em `constants.js` e nos scripts específicos de cada página.

## Principais funcionalidades

- **Home**: duas abas
  - **Memory**: grade com 12 quadrados que podem receber “cores” (imagens) para marcação manual.
  - **Quiz**: filtro de frases (V/F) por texto, ignorando acentos.
- **Receitas**: lista de comidas + cálculo automático de custo total (berries) por quantidade.
- **Baús e Conquistas**: catálogo por ilha (baús) e lista de conquistas.
- **World Boss Ranking**: ranking por boss e por data.
- Páginas adicionais (ferramentas): **Mapa Interativo**, **Planejador de Diamantes**, **Planejador de Coliseu**, **Criador de Grupo (TeamBuilder)**, **Rotations**, **To Do List**, **Glaguessr**.

## Onde ficam os dados

- A maior parte do “banco de dados” fica em `constants.js` (itens, ilhas/mapas, baús, ovos, conquistas, foods/ingredientes, world bosses, rotações).
- Algumas páginas mantêm seus próprios datasets (ex.: `dima.js`, `teambuilder.js`, `coliseum.js`).

## Estado/persistência

- **`localStorage`**:
  - `markedChests` e `markedEggs` (Mapa Interativo)
  - `accounts` (To Do List)
- **URL**:
  - Hash `#memory`/`#quiz` (Home)
  - Query `?chars=...` (Planejador de Coliseu, para compartilhar link)

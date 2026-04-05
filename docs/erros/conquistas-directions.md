# Conquistas: `directions` não renderiza imagens

## Sintoma

- Ao selecionar uma conquista na Home, o app cria “espaços”/elementos para imagens de `directions`, mas **nenhuma imagem aparece**.

## Onde ocorre

- Criação de `<img>` sem atribuir `src` em [index.js](index.js#L4584-L4588).

## Causa

- O loop itera `achiev.directions`, mas apenas cria o elemento e adiciona classe; não faz `imgElement.src = ...`.

## Impacto

- Informações visuais de passo-a-passo (quando existirem em `directions`) não são exibidas.

## Correção recomendada

- Atribuir `src` com o valor iterado, por exemplo:
  - `imgElement.src = img`
- Garantir que os paths em `achievements[].directions[]` apontem para arquivos existentes em `Img/Achievs/` (ou outro diretório de imagens).

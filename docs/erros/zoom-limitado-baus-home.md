# Baús (Home): zoom desejado limitado por `maxZoom`

## Sintoma

- Ao abrir o mapa de um baú na Home, o app tenta centralizar e aplicar zoom (ex.: `2.5`), mas o zoom fica travado e não passa de `1`.

## Onde ocorre

- `maxZoom = 1` em [index.js](index.js#L4247).
- O zoom é limitado por `Math.min(..., maxZoom)` em [index.js](index.js#L4357).
- A centralização chama `centerMapOnChest(chest, 2.5)` em [index.js](index.js#L4499).

## Causa

- O valor máximo de zoom está configurado como `1`, então qualquer “zoom desejado” maior é truncado.

## Impacto

- UX pior para visualizar baús em mapas grandes/cheios de detalhes.

## Correção recomendada

- Aumentar `maxZoom` para um valor > 1 (ex.: 3 ou 4), ou tornar isso configurável.
- Se existir motivo para limitar a 1, remover/ajustar as chamadas que pedem zoom maior para não gerar expectativa de zoom.

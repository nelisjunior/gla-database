# Baús (Home): `click` listener criado dentro do `mousemove`

## Sintoma

- O mapa de baús na Home pode ficar mais lento com o tempo.
- Um clique pode disparar múltiplos logs/efeitos, dependendo de quantos listeners foram anexados.

## Onde ocorre

- O `click` listener é criado dentro do handler de `mousemove` em [index.js](index.js#L4532-L4561).

## Causa

- Cada evento de `mousemove` executa `chestMap.addEventListener('click', ...)`, anexando **mais um** listener.

## Impacto

- Crescimento não-controlado de listeners (risco de degradar performance e comportamento inesperado).

## Correção recomendada

- Mover o `addEventListener('click', ...)` para fora do `mousemove`.
- Se o objetivo for apenas debugar coordenadas, considerar:
  - logar no próprio `mousemove` sob uma flag, ou
  - usar um único listener de `click` que lê as coordenadas atuais calculadas.

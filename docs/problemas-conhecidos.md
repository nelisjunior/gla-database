# Problemas Conhecidos / Pontos de Atenção

Este arquivo lista achados da análise que podem afetar manutenção ou execução.

## Detalhamento

Os detalhes (com sintomas, impacto e correção recomendada) ficam em:

- `docs/erros/README.md`

## Lista resumida

- Paths case-sensitive: `Img/maps` vs `Img/Maps` (Glaguessr)
- Conquistas: `directions` cria `<img>` sem `src`
- Baús (Home): zoom limitado por `maxZoom = 1`
- Baús (Home): `click` listener adicionado dentro de `mousemove`
- README antigo em UTF-16 (substituído por UTF-8)

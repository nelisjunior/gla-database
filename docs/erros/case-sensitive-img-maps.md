# Paths com maiúsculas/minúsculas (Img/maps vs Img/Maps)

## Sintoma

- No Linux (e outros ambientes case-sensitive), as imagens de algumas ilhas **não carregam** no Glaguessr.

## Onde ocorre

- Referência com diretório em minúsculo em [glaguessr.js](glaguessr.js#L124).
- O restante do projeto (e os assets) usa `Img/Maps/` (ex.: [map.js](map.js#L40)).

## Causa

- Divergência no caminho do diretório: `Img/maps/` (minúsculo) não existe no repositório; o diretório real é `Img/Maps/`.

## Impacto

- Ícones/imagens de ilha podem ficar quebrados no Glaguessr.

## Como reproduzir

- Abrir `glaguessr.html` em um host Linux.
- Selecionar uma ilha e observar no Network/Console que o request para `Img/maps/...` retorna 404.

## Correção recomendada

- Trocar `Img/maps/` para `Img/Maps/` no Glaguessr.
- Opcional (mais robusto): padronizar todos os paths de imagens do projeto para a mesma capitalização.
